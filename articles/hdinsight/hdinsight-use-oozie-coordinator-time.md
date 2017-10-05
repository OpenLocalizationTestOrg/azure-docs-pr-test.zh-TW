---
title: "在 HDInsight 上使用以時間為基礎的 Hadoop Oozie 協調器 | Microsoft Docs"
description: "在 HDInsight 上使用以時間為基礎的 Hadoop Oozie 協調器：一項巨量資料服務。 了解如何定義 Oozie 工作流程和協調器，以及提交工作。"
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
ms.openlocfilehash: 600a70c74a16e2601a874f804ac2e8382c8bfa90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="f847f-104">在 HDInsight 上將以時間為基礎的 Oozie 協調器與 Hadoop 搭配使用，以定義工作流程和協調工作</span><span class="sxs-lookup"><span data-stu-id="f847f-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="f847f-105">在本文中，您將了解如何定義工作流程和協調器，以及如何觸發以時間為基礎的協調器工作。</span><span class="sxs-lookup"><span data-stu-id="f847f-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="f847f-106">閱讀本文之前，建議先看過一遍[搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]。</span><span class="sxs-lookup"><span data-stu-id="f847f-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="f847f-107">除了 Oozie，您也可以使用 Azure Data Factory 排定工作。</span><span class="sxs-lookup"><span data-stu-id="f847f-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="f847f-108">若要了解 Azure Data Factory，請參閱 [搭配 Data Factory 使用 Pig 和 Hive](../data-factory/data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="f847f-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f847f-109">本文章需有以 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f847f-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="f847f-110">如需在以 Linux 為基礎之叢集上使用 Oozie (包括以時間為基礎的作業) 的相關資訊，請參閱 [在以 Linux 為基礎的 HDInsight 上搭配 Hadoop 使用 Oozie 來定義並執行工作流程](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="f847f-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="f847f-111">什麼是 Oozie</span><span class="sxs-lookup"><span data-stu-id="f847f-111">What is Oozie</span></span>
<span data-ttu-id="f847f-112">Apache Oozie 是可管理 Hadoop 工作的工作流程/協調系統。</span><span class="sxs-lookup"><span data-stu-id="f847f-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="f847f-113">它可與 Hadoop 堆疊相整合，並支援 Apache MapReduce、Apache Pig、Apache Hive 和 Apache Sqoop 的 Hadoop 工作。</span><span class="sxs-lookup"><span data-stu-id="f847f-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="f847f-114">它也可用來排程系統的特定工作，例如 Java 程式或 Shell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f847f-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="f847f-115">下圖說明您將實作的工作流程：</span><span class="sxs-lookup"><span data-stu-id="f847f-115">The following image shows the workflow you will implement:</span></span>

![Workflow diagram][img-workflow-diagram]

<span data-ttu-id="f847f-117">此工作流程有兩個動作：</span><span class="sxs-lookup"><span data-stu-id="f847f-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="f847f-118">Hive 動作會執行一個 HiveQL 指令碼，藉此計算每個記錄層級類型在 log4j 記錄檔中的出現次數。</span><span class="sxs-lookup"><span data-stu-id="f847f-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="f847f-119">每個 log4j 記錄各由一列欄位組成，其中包括顯示類型和嚴重性的 [LOG LEVEL] 欄位，例如：</span><span class="sxs-lookup"><span data-stu-id="f847f-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="f847f-120">Hive 指令碼輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f847f-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="f847f-121">如需 Hive 的詳細資訊，請參閱[在 HDInsight 上使用 Hive][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="f847f-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="f847f-122">Sqoop 動作會將 HiveQL 動作的輸出匯出至 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="f847f-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="f847f-123">如需 Sqoop 的詳細資訊，請參閱[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]。</span><span class="sxs-lookup"><span data-stu-id="f847f-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="f847f-124">如需 HDInsight 叢集支援的 Oozie 版本，請參閱 [HDInsight 提供的叢集版本有哪些新功能？][hdinsight-versions]。</span><span class="sxs-lookup"><span data-stu-id="f847f-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="f847f-125">必要條件</span><span class="sxs-lookup"><span data-stu-id="f847f-125">Prerequisites</span></span>
<span data-ttu-id="f847f-126">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="f847f-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="f847f-127">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="f847f-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f847f-128">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，將會在 2017 年 1 月 1 日前移除。</span><span class="sxs-lookup"><span data-stu-id="f847f-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="f847f-129">本文件中的步驟會使用可與 Azure Resource Manager 搭配使用的新 HDInsight Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f847f-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="f847f-130">請遵循 [安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) 中的步驟來安裝最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f847f-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="f847f-131">如果您需要修改指令碼才能使用適用於 Azure Resource Manager 的新 Cmdlet，請參閱 [移轉至以 Azure Resource Manager 為基礎的開發工具 (適用於 HDInsight 叢集)](hdinsight-hadoop-development-using-azure-resource-manager.md) ，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f847f-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="f847f-132">**HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="f847f-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="f847f-133">如需關於建立 HDInsight 叢集的詳細資訊，請參閱[建立 HDInsight 叢集][hdinsight-provision]或[開始使用 HDInsight][hdinsight-get-started]。</span><span class="sxs-lookup"><span data-stu-id="f847f-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="f847f-134">進行教學課程時，您將需要下列資料：</span><span class="sxs-lookup"><span data-stu-id="f847f-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="f847f-135">叢集屬性</span><span class="sxs-lookup"><span data-stu-id="f847f-135">Cluster property</span></span></th><th><span data-ttu-id="f847f-136">Windows PowerShell 變數名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="f847f-137">值</span><span class="sxs-lookup"><span data-stu-id="f847f-137">Value</span></span></th><th><span data-ttu-id="f847f-138">說明</span><span class="sxs-lookup"><span data-stu-id="f847f-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="f847f-139">HDInsight 叢集名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="f847f-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="f847f-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="f847f-141">您將用來執行此教學課程的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f847f-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-142">HDInsight 叢集使用者名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="f847f-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="f847f-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="f847f-144">HDInsight 叢集使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f847f-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="f847f-145">HDInsight 叢集使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="f847f-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="f847f-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="f847f-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="f847f-147">HDInsight 叢集使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="f847f-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-148">Azure 儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-148">Azure storage account name</span></span></td><td><span data-ttu-id="f847f-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="f847f-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="f847f-150">可供 HDInsight 叢集使用的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f847f-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="f847f-151">在本教學課程中，請使用在叢集佈建程序中指定的預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f847f-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-152">Azure Blob 容器名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-152">Azure Blob container name</span></span></td><td><span data-ttu-id="f847f-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="f847f-153">$containerName</span></span></td><td></td><td><span data-ttu-id="f847f-154">在此範例中，請使用預設 HDInsight 叢集檔案系統所使用的 Azure Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="f847f-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="f847f-155">根據預設，此容器的名稱會與 HDInsight 叢集名稱相同。</span><span class="sxs-lookup"><span data-stu-id="f847f-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="f847f-156">
* **Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="f847f-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="f847f-157">您必須設定 SQL Database Server 的防火牆規則，以允許從您的工作站加以存取。</span><span class="sxs-lookup"><span data-stu-id="f847f-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="f847f-158">如需建立 Azure SQL Database 以及設定防火牆的指示，請參閱[開始使用 Azure SQL Database][sqldatabase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="f847f-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="f847f-159">本文會提供 Windows PowerShell 指令碼，以建立本教學課程所需的 Azure SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="f847f-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="f847f-160">SQL Database 屬性</span><span class="sxs-lookup"><span data-stu-id="f847f-160">SQL database property</span></span></th><th><span data-ttu-id="f847f-161">Windows PowerShell 變數名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="f847f-162">值</span><span class="sxs-lookup"><span data-stu-id="f847f-162">Value</span></span></th><th><span data-ttu-id="f847f-163">說明</span><span class="sxs-lookup"><span data-stu-id="f847f-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="f847f-164">SQL Database 伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-164">SQL database server name</span></span></td><td><span data-ttu-id="f847f-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="f847f-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="f847f-166">Sqoop 會將資料匯出至其中的 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f847f-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="f847f-167">SQL Database 登入名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-167">SQL database login name</span></span></td><td><span data-ttu-id="f847f-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="f847f-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="f847f-169">SQL Database 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="f847f-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-170">SQL Database 登入密碼</span><span class="sxs-lookup"><span data-stu-id="f847f-170">SQL database login password</span></span></td><td><span data-ttu-id="f847f-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="f847f-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="f847f-172">SQL Database 登入密碼。</span><span class="sxs-lookup"><span data-stu-id="f847f-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-173">SQL Database 名稱</span><span class="sxs-lookup"><span data-stu-id="f847f-173">SQL database name</span></span></td><td><span data-ttu-id="f847f-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="f847f-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="f847f-175">Sqoop 會將資料匯出至其中的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f847f-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="f847f-176">根據預設，Azure SQL Database 接受來自 Azure 服務 (例如 Azure HDInsight) 的連線。</span><span class="sxs-lookup"><span data-stu-id="f847f-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="f847f-177">如果此防火牆設定為停用，您必須在 Azure 入口網站中加以啟用。</span><span class="sxs-lookup"><span data-stu-id="f847f-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="f847f-178">如需關於建立 SQL Database 和設定防火牆規則的指示，請參閱[建立和設定 SQL Database][sqldatabase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="f847f-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="f847f-179">在資料表中填入值。</span><span class="sxs-lookup"><span data-stu-id="f847f-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="f847f-180">這將有助於本教學課程的執行。</span><span class="sxs-lookup"><span data-stu-id="f847f-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="f847f-181">定義 Oozie 工作流程和相關的 HiveQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="f847f-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="f847f-182">Oozie 工作流程定義會以 hPDL 撰寫 (一種 XML 程序定義語言)。</span><span class="sxs-lookup"><span data-stu-id="f847f-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="f847f-183">預設的工作流程檔案名稱為 *workflow.xml*。</span><span class="sxs-lookup"><span data-stu-id="f847f-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="f847f-184">您將在本機儲存工作流程檔案，然後在本教學課程中使用 Azure PowerShell 將該工作流程部署至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f847f-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="f847f-185">此工作流程中的 Hive 動作會呼叫 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="f847f-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="f847f-186">此指令碼檔案包含三個 HiveQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="f847f-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="f847f-187">**DROP TABLE 陳述式** 會刪除 log4j Hive 資料表 (如果資料表存在)。</span><span class="sxs-lookup"><span data-stu-id="f847f-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="f847f-188">**CREATE TABLE 陳述式** 會建立指向 log4j 記錄檔位置的 log4j Hive 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="f847f-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="f847f-189">**log4j 記錄檔的位置**。</span><span class="sxs-lookup"><span data-stu-id="f847f-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="f847f-190">欄位分隔符號為 ","。</span><span class="sxs-lookup"><span data-stu-id="f847f-190">The field delimiter is ",".</span></span> <span data-ttu-id="f847f-191">預設的行分隔符號為 "\n"。</span><span class="sxs-lookup"><span data-stu-id="f847f-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="f847f-192">Hive 外部資料表可讓您在需要執行 Oozie 工作流程多次時，避免資料檔案從原始位置遭到移除。</span><span class="sxs-lookup"><span data-stu-id="f847f-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="f847f-193">**INSERT OVERWRITE 陳述式** 可從 log4j Hive 資料表中計算每個記錄層級類型的出現次數，並將輸出儲存至 Azure Blob 儲存體的位置。</span><span class="sxs-lookup"><span data-stu-id="f847f-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="f847f-194">Hive 路徑有已知問題。</span><span class="sxs-lookup"><span data-stu-id="f847f-194">There is a known Hive path issue.</span></span> <span data-ttu-id="f847f-195">此問題會在您提交 Oozie 工作時發生。</span><span class="sxs-lookup"><span data-stu-id="f847f-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="f847f-196">如需修正此問題的指示，請參閱 TechNet Wiki：[HDInsight Hive 錯誤：無法重新命名][technetwiki-hive-error]。</span><span class="sxs-lookup"><span data-stu-id="f847f-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="f847f-197">**定義要由工作流程呼叫的 HiveQL 指令碼檔案**</span><span class="sxs-lookup"><span data-stu-id="f847f-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="f847f-198">建立含有下列內容的文字檔：</span><span class="sxs-lookup"><span data-stu-id="f847f-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="f847f-199">指令碼中使用三種變數：</span><span class="sxs-lookup"><span data-stu-id="f847f-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="f847f-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="f847f-200">${hiveTableName}</span></span>
   * <span data-ttu-id="f847f-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="f847f-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="f847f-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="f847f-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="f847f-203">工作流程定義檔 (在本教學課程中為 workflow.xml) 會在執行階段將這些值傳遞至此 HiveQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f847f-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="f847f-204">使用 ANSI (ASCII) 編碼將檔案另存為 **C:\Tutorials\UseOozie\useooziewf.hql**。</span><span class="sxs-lookup"><span data-stu-id="f847f-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="f847f-205">(如果您的文字編輯器沒有此選項，請使用「記事本」)。稍後本教學課程會將此指令碼檔案部署至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f847f-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="f847f-206">**定義工作流程**</span><span class="sxs-lookup"><span data-stu-id="f847f-206">**To define a workflow**</span></span>

1. <span data-ttu-id="f847f-207">建立含有下列內容的文字檔：</span><span class="sxs-lookup"><span data-stu-id="f847f-207">Create a text file with the following content:</span></span>

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

    <span data-ttu-id="f847f-208">此工作流程中定義了兩個動作。</span><span class="sxs-lookup"><span data-stu-id="f847f-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="f847f-209">起始動作為 *RunHiveScript*。</span><span class="sxs-lookup"><span data-stu-id="f847f-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="f847f-210">如果此動作「順利」執行，則下一個動作為 *RunSqoopExport*。</span><span class="sxs-lookup"><span data-stu-id="f847f-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="f847f-211">RunHiveScript 有數個變數。</span><span class="sxs-lookup"><span data-stu-id="f847f-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="f847f-212">當您使用 Azure PowerShell 從工作站提交 Oozie 工作時，要傳入這些值。</span><span class="sxs-lookup"><span data-stu-id="f847f-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="f847f-213">工作流程變數</span><span class="sxs-lookup"><span data-stu-id="f847f-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="f847f-214">工作流程變數</span><span class="sxs-lookup"><span data-stu-id="f847f-214">Workflow variables</span></span></th><th><span data-ttu-id="f847f-215">說明</span><span class="sxs-lookup"><span data-stu-id="f847f-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="f847f-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="f847f-216">${jobTracker}</span></span></td><td><span data-ttu-id="f847f-217">指定 Hadoop 工作追蹤器的 URL。</span><span class="sxs-lookup"><span data-stu-id="f847f-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="f847f-218">請在 HDInsight 叢集 3.0 和 2.0 版上使用 <strong>jobtrackerhost:9010</strong>。</span><span class="sxs-lookup"><span data-stu-id="f847f-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="f847f-219">${nameNode}</span></span></td><td><span data-ttu-id="f847f-220">指定 Hadoop 名稱節點的 URL。</span><span class="sxs-lookup"><span data-stu-id="f847f-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="f847f-221">使用預設檔案系統 wasb:// 位址，例如 <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>。</span><span class="sxs-lookup"><span data-stu-id="f847f-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="f847f-222">${queueName}</span></span></td><td><span data-ttu-id="f847f-223">指定要將工作提交過去的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="f847f-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="f847f-224">使用<strong>預設值</strong>。</span><span class="sxs-lookup"><span data-stu-id="f847f-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="f847f-225">Hive 動作變數</span><span class="sxs-lookup"><span data-stu-id="f847f-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="f847f-226">Hive 動作變數</span><span class="sxs-lookup"><span data-stu-id="f847f-226">Hive action variable</span></span></th><th><span data-ttu-id="f847f-227">說明</span><span class="sxs-lookup"><span data-stu-id="f847f-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="f847f-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="f847f-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="f847f-229">Hive Create Table 命令的來源目錄。</span><span class="sxs-lookup"><span data-stu-id="f847f-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="f847f-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="f847f-231">INSERT OVERWRITE 陳述式的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="f847f-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="f847f-232">${hiveTableName}</span></span></td><td><span data-ttu-id="f847f-233">參考 log4j 資料檔案之 Hive 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="f847f-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="f847f-234">Sqoop 動作變數</span><span class="sxs-lookup"><span data-stu-id="f847f-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="f847f-235">Sqoop 動作變數</span><span class="sxs-lookup"><span data-stu-id="f847f-235">Sqoop action variable</span></span></th><th><span data-ttu-id="f847f-236">說明</span><span class="sxs-lookup"><span data-stu-id="f847f-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="f847f-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="f847f-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="f847f-238">SQL Database 連接字串。</span><span class="sxs-lookup"><span data-stu-id="f847f-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="f847f-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="f847f-240">要匯入資料的 Azure SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="f847f-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="f847f-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="f847f-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="f847f-242">Hive INSERT OVERWRITE 陳述式的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="f847f-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="f847f-243">這是 Sqoop 匯出 (export-dir) 的相同資料夾。</span><span class="sxs-lookup"><span data-stu-id="f847f-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="f847f-244">如需關於 Oozie 工作流程和使用工作流程動作的詳細資訊，請參閱 [Apache Oozie 4.0 文件][apache-oozie-400] (適用於 HDInsight 叢集 3.0 版) 或 [Apache Oozie 3.3.2 文件][apache-oozie-332] (適用於 HDInsight 叢集 2.1 版)。</span><span class="sxs-lookup"><span data-stu-id="f847f-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="f847f-245">使用 ANSI (ASCII) 編碼將檔案另存為 **C:\Tutorials\UseOozie\workflow.xml**。</span><span class="sxs-lookup"><span data-stu-id="f847f-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="f847f-246">(如果您的文字編輯器沒有此選項，請使用「記事本」)。</span><span class="sxs-lookup"><span data-stu-id="f847f-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="f847f-247">**定義協調器**</span><span class="sxs-lookup"><span data-stu-id="f847f-247">**To define coordinator**</span></span>

1. <span data-ttu-id="f847f-248">建立含有下列內容的文字檔：</span><span class="sxs-lookup"><span data-stu-id="f847f-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="f847f-249">定義檔中使用五種變數：</span><span class="sxs-lookup"><span data-stu-id="f847f-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="f847f-250">變數</span><span class="sxs-lookup"><span data-stu-id="f847f-250">Variable</span></span> | <span data-ttu-id="f847f-251">說明</span><span class="sxs-lookup"><span data-stu-id="f847f-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="f847f-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="f847f-252">${coordFrequency}</span></span> |<span data-ttu-id="f847f-253">工作暫停時間。</span><span class="sxs-lookup"><span data-stu-id="f847f-253">Job pause time.</span></span> <span data-ttu-id="f847f-254">頻率一律以分鐘表示。</span><span class="sxs-lookup"><span data-stu-id="f847f-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="f847f-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="f847f-255">${coordStart}</span></span> |<span data-ttu-id="f847f-256">工作開始時間。</span><span class="sxs-lookup"><span data-stu-id="f847f-256">Job start time.</span></span> |
   | <span data-ttu-id="f847f-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="f847f-257">${coordEnd}</span></span> |<span data-ttu-id="f847f-258">工作結束時間。</span><span class="sxs-lookup"><span data-stu-id="f847f-258">Job end time.</span></span> |
   | <span data-ttu-id="f847f-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="f847f-259">${coordTimezone}</span></span> |<span data-ttu-id="f847f-260">Oozie 在固定時區處理協調器工作，不受日光節約時間影響 (通常使用 UTC 表示)。</span><span class="sxs-lookup"><span data-stu-id="f847f-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="f847f-261">此時區稱為「Oozie 處理時區」。</span><span class="sxs-lookup"><span data-stu-id="f847f-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="f847f-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="f847f-262">${wfPath}</span></span> |<span data-ttu-id="f847f-263">workflow.xml 的路徑。</span><span class="sxs-lookup"><span data-stu-id="f847f-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="f847f-264">如果工作流程檔案名稱不是預設檔案名稱 (workflow.xml)，您必須加以指定。</span><span class="sxs-lookup"><span data-stu-id="f847f-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="f847f-265">使用 ANSI (ASCII) 編碼將檔案另存為 **C:\Tutorials\UseOozie\coordinator.xml**。</span><span class="sxs-lookup"><span data-stu-id="f847f-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="f847f-266">(如果您的文字編輯器沒有此選項，請使用「記事本」)。</span><span class="sxs-lookup"><span data-stu-id="f847f-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="f847f-267">部署 Oozie 專案及進行教學課程前置工作</span><span class="sxs-lookup"><span data-stu-id="f847f-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="f847f-268">您將執行 Azure PowerShell 指令碼，以執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="f847f-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="f847f-269">將 HiveQL 指令碼 (useoozie.hql) 複製到 Azure Blob 儲存體 wasb:///tutorials/useoozie/useoozie.hql。</span><span class="sxs-lookup"><span data-stu-id="f847f-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="f847f-270">將 workflow.xml 複製到 wasb:///tutorials/useoozie/workflow.xml。</span><span class="sxs-lookup"><span data-stu-id="f847f-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="f847f-271">將 coordinator.xml 複製到 wasb:///tutorials/useoozie/coordinator.xml。</span><span class="sxs-lookup"><span data-stu-id="f847f-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="f847f-272">將資料檔案 (/example/data/sample.log) 複製到 wasb:///tutorials/useoozie/data/sample.log。</span><span class="sxs-lookup"><span data-stu-id="f847f-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="f847f-273">建立用於儲存 Sqoop 匯出資料的 Azure SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="f847f-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="f847f-274">資料表名稱為 *log4jLogCount*。</span><span class="sxs-lookup"><span data-stu-id="f847f-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="f847f-275">**了解 HDInsight 儲存體**</span><span class="sxs-lookup"><span data-stu-id="f847f-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="f847f-276">HDInsight 使用 Azure Blob 儲存體來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="f847f-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="f847f-277">wasb:// 是 Azure Blob 儲存體中 Hadoop 分散式檔案系統 (HDFS) 的 Microsoft 實作。</span><span class="sxs-lookup"><span data-stu-id="f847f-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="f847f-278">如需詳細資訊，請參閱[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]。</span><span class="sxs-lookup"><span data-stu-id="f847f-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="f847f-279">當您佈建 HDInsight 叢集時，會將一個 Azure Blob 儲存體帳戶及該帳戶下的特定 Blob 容器指定為預設檔案系統，如同在 HDFS 中一般。</span><span class="sxs-lookup"><span data-stu-id="f847f-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="f847f-280">除了此儲存體帳戶之外，您也可以在佈建過程中，從相同的 Azure 訂用帳戶或不同 Azure 訂用帳戶新增其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f847f-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="f847f-281">如需關於新增其他儲存體帳戶的指示，請參閱[佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="f847f-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="f847f-282">為簡化本教學課程中使用的 PowerShell 指令碼，所有檔案都會儲存在位於 */tutorials/useoozie*的預設檔案系統容器中。</span><span class="sxs-lookup"><span data-stu-id="f847f-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="f847f-283">根據預設，此容器的名稱會與 HDInsight 叢集名稱相同。</span><span class="sxs-lookup"><span data-stu-id="f847f-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="f847f-284">語法為：</span><span class="sxs-lookup"><span data-stu-id="f847f-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="f847f-285">HDInsight 叢集 3.0 版僅支援「wasb://」語法。</span><span class="sxs-lookup"><span data-stu-id="f847f-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="f847f-286">HDInsight 2.1 和 1.6 叢集支援舊的「asv://」語法，但在 HDInsight 3.0 叢集中不支援。</span><span class="sxs-lookup"><span data-stu-id="f847f-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="f847f-287">wasb:// 路徑為虛擬路徑。</span><span class="sxs-lookup"><span data-stu-id="f847f-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="f847f-288">如需詳細資訊，請參閱[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]。</span><span class="sxs-lookup"><span data-stu-id="f847f-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="f847f-289">您可以使用下列任一 URI (我使用 workflow.xml 做為範例)，從 HDInsight 存取儲存在預設檔案系統容器中的檔案：</span><span class="sxs-lookup"><span data-stu-id="f847f-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="f847f-290">如果您要直接從儲存體帳戶存取檔案，檔案的Blob 名稱為：</span><span class="sxs-lookup"><span data-stu-id="f847f-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="f847f-291">**了解 Hive 內部和外部資料表**</span><span class="sxs-lookup"><span data-stu-id="f847f-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="f847f-292">關於 Hive 內部資料表和外部資料表，有若干事項您必須了解：</span><span class="sxs-lookup"><span data-stu-id="f847f-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="f847f-293">CREATE TABLE 命令會建立內部資料表，也稱為受管理的資料表。</span><span class="sxs-lookup"><span data-stu-id="f847f-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="f847f-294">資料檔案必須位於預設容器中。</span><span class="sxs-lookup"><span data-stu-id="f847f-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="f847f-295">CREATE TABLE 命令會將資料檔案移至預設容器中的 /hive/warehouse/<TableName> 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f847f-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="f847f-296">CREATE EXTERNAL TABLE 命令會建立外部資料表。</span><span class="sxs-lookup"><span data-stu-id="f847f-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="f847f-297">資料檔案可位於預設容器外。</span><span class="sxs-lookup"><span data-stu-id="f847f-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="f847f-298">CREATE EXTERNAL TABLE 命令不會移動資料檔案。</span><span class="sxs-lookup"><span data-stu-id="f847f-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="f847f-299">CREATE EXTERNAL TABLE 命令不允許在 LOCATION 子句中指定的資料夾下放置任何子資料夾。</span><span class="sxs-lookup"><span data-stu-id="f847f-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="f847f-300">因此，此教學課程複製了 sample.log 檔案。</span><span class="sxs-lookup"><span data-stu-id="f847f-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="f847f-301">如需詳細資訊，請參閱 [HDInsight：Hive 內部和外部資料表簡介][cindygross-hive-tables]。</span><span class="sxs-lookup"><span data-stu-id="f847f-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="f847f-302">**教學課程前置工作**</span><span class="sxs-lookup"><span data-stu-id="f847f-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="f847f-303">開啟 Windows PowerShell ISE (在 Windows 8 的 [開始] 畫面上輸入 **PowerShell_ISE**，然後按一下 [Windows PowerShell ISE]。</span><span class="sxs-lookup"><span data-stu-id="f847f-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="f847f-304">如需詳細資訊，請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start])。</span><span class="sxs-lookup"><span data-stu-id="f847f-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="f847f-305">在底部窗格中執行下列命令，以連接到您的 Azure 訂閱：</span><span class="sxs-lookup"><span data-stu-id="f847f-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="f847f-306">系統會提示您輸入 Azure 帳號認證。</span><span class="sxs-lookup"><span data-stu-id="f847f-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="f847f-307">這種新增訂用帳戶連線的方法會逾時，且在 12 小時後，您將必須重新執行 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f847f-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f847f-308">如果您有多個 Azure 訂用帳戶，且預設訂用帳戶並非您要使用的訂用帳戶，請使用 <strong>Select-AzureSubscription</strong> Cmdlet 來選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f847f-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="f847f-309">將以下指令碼複製到指令碼窗格中，然後設定前六個變數：</span><span class="sxs-lookup"><span data-stu-id="f847f-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

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

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="f847f-310">如需變數的詳細說明，請參閱本教學課程中的 [必要條件](#prerequisites) 一節。</span><span class="sxs-lookup"><span data-stu-id="f847f-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="f847f-311">將下列程式碼附加到指令碼窗格中的指令碼：</span><span class="sxs-lookup"><span data-stu-id="f847f-311">Append the following to the script in the script pane:</span></span>

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
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
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

        #Create the log4jLogsCount table
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

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="f847f-312">按一下 [執行指令碼] 或按 [F5]，以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f847f-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="f847f-313">輸出將類似於：</span><span class="sxs-lookup"><span data-stu-id="f847f-313">The output will be similar to:</span></span>

    ![Tutorial preparation output][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="f847f-315">執行 Oozie 專案</span><span class="sxs-lookup"><span data-stu-id="f847f-315">Run the Oozie project</span></span>
<span data-ttu-id="f847f-316">Azure PowerShell 目前並未提供任何用以定義 Oozie 工作的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f847f-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="f847f-317">您可以使用 **Invoke-RestMethod** Cmdlet 來叫用 Oozie Web 服務。</span><span class="sxs-lookup"><span data-stu-id="f847f-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="f847f-318">Oozie Web 服務 API 是 HTTP REST JSON API。</span><span class="sxs-lookup"><span data-stu-id="f847f-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="f847f-319">如需關於 Oozie Web 服務 API 的詳細資訊，請參閱 [Apache Oozie 4.0 文件][apache-oozie-400] (適用於 HDInsight 叢集 3.0 版) 或 [Apache Oozie 3.3.2 文件][apache-oozie-332] (適用於 HDInsight 叢集 2.1 版)。</span><span class="sxs-lookup"><span data-stu-id="f847f-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="f847f-320">**提交 Oozie 工作**</span><span class="sxs-lookup"><span data-stu-id="f847f-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="f847f-321">開啟 Windows PowerShell ISE (在 Windows 8 的 [開始] 畫面上輸入 **PowerShell_ISE**，然後按一下 [Windows PowerShell ISE]。</span><span class="sxs-lookup"><span data-stu-id="f847f-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="f847f-322">如需詳細資訊，請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start])。</span><span class="sxs-lookup"><span data-stu-id="f847f-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="f847f-323">將以下指令碼複製到指令碼窗格中，然後設定前十四個變數 (但請略過 **$storageUri**)。</span><span class="sxs-lookup"><span data-stu-id="f847f-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

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

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
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

    <span data-ttu-id="f847f-324">如需變數的詳細說明，請參閱本教學課程中的 [必要條件](#prerequisites) 一節。</span><span class="sxs-lookup"><span data-stu-id="f847f-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="f847f-325">$coordstart 和 $coordend 是工作流程的開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="f847f-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="f847f-326">若要找出 UTC/GMT 時間，請在 bing.com 搜尋「utc 時間」。$coordFrequency 是您要執行工作流程的頻率 (以分鐘為單位)。</span><span class="sxs-lookup"><span data-stu-id="f847f-326">To find out the UTC/GMT time, search "utc time" on bing.com. The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="f847f-327">將下列程式碼附加至指令碼：</span><span class="sxs-lookup"><span data-stu-id="f847f-327">Append the following to the script.</span></span> <span data-ttu-id="f847f-328">這部分會定義 Oozie 裝載：</span><span class="sxs-lookup"><span data-stu-id="f847f-328">This part defines the Oozie payload:</span></span>

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
   > <span data-ttu-id="f847f-329">與工作流程提交裝載檔案的主要差異在於變數 **oozie.coord.application.path**。</span><span class="sxs-lookup"><span data-stu-id="f847f-329">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="f847f-330">提交工作流程工作時，您必須改用 **oozie.wf.application.path** 。</span><span class="sxs-lookup"><span data-stu-id="f847f-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="f847f-331">將下列程式碼附加至指令碼：</span><span class="sxs-lookup"><span data-stu-id="f847f-331">Append the following to the script.</span></span> <span data-ttu-id="f847f-332">這部分會檢查 Oozie Web 服務狀態：</span><span class="sxs-lookup"><span data-stu-id="f847f-332">This part checks the Oozie web service status:</span></span>

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
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="f847f-333">將下列程式碼附加至指令碼：</span><span class="sxs-lookup"><span data-stu-id="f847f-333">Append the following to the script.</span></span> <span data-ttu-id="f847f-334">這部分會建立 Oozie 工作：</span><span class="sxs-lookup"><span data-stu-id="f847f-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
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
   > <span data-ttu-id="f847f-335">提交工作流程工作時，您必須在工作建立後發出另一個 Web 服務呼叫，以啟動工作。</span><span class="sxs-lookup"><span data-stu-id="f847f-335">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="f847f-336">在此情況下，協調器工作會依時間觸發。</span><span class="sxs-lookup"><span data-stu-id="f847f-336">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="f847f-337">工作將會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="f847f-337">The job will start automatically.</span></span>

6. <span data-ttu-id="f847f-338">將下列程式碼附加至指令碼：</span><span class="sxs-lookup"><span data-stu-id="f847f-338">Append the following to the script.</span></span> <span data-ttu-id="f847f-339">這部分會檢查 Oozie 工作狀態：</span><span class="sxs-lookup"><span data-stu-id="f847f-339">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
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

7. <span data-ttu-id="f847f-340">(選用) 將下列程式碼附加至指令碼。</span><span class="sxs-lookup"><span data-stu-id="f847f-340">(Optional) Append the following to the script.</span></span>

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
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="f847f-341">將下列程式碼附加至指令碼：</span><span class="sxs-lookup"><span data-stu-id="f847f-341">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="f847f-342">Remove the # signs if you want to run the additional functions.</span><span class="sxs-lookup"><span data-stu-id="f847f-342">Remove the # signs if you want to run the additional functions.</span></span>
9. <span data-ttu-id="f847f-343">如果您的 HDinsight 叢集是 2.1 版，請將 "https://$clusterName.azurehdinsight.net:443/oozie/v2/" 取代為 "https://$clusterName.azurehdinsight.net:443/oozie/v1/"。</span><span class="sxs-lookup"><span data-stu-id="f847f-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="f847f-344">HDInsight 叢集 2.1 版不支援 Web 服務的第 2 版。</span><span class="sxs-lookup"><span data-stu-id="f847f-344">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="f847f-345">按一下 [執行指令碼] 或按 [F5]，以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f847f-345">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="f847f-346">輸出將類似於：</span><span class="sxs-lookup"><span data-stu-id="f847f-346">The output will be similar to:</span></span>

     ![Tutorial run workflow output][img-runworkflow-output]
11. <span data-ttu-id="f847f-348">連接到您的 SQL Database，以檢視匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="f847f-348">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="f847f-349">**檢查工作錯誤記錄**</span><span class="sxs-lookup"><span data-stu-id="f847f-349">**To check the job error log**</span></span>

<span data-ttu-id="f847f-350">若要進行工作流程的疑難排解，您可以從叢集前端節點，找出位於 C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log 的 Oozie 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f847f-350">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="f847f-351">如需 RDP 的資訊，請參閱[使用 Azure 入口網站管理 HDInsight 叢集][hdinsight-admin-portal]。</span><span class="sxs-lookup"><span data-stu-id="f847f-351">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="f847f-352">**重新執行教學課程**</span><span class="sxs-lookup"><span data-stu-id="f847f-352">**To rerun the tutorial**</span></span>

<span data-ttu-id="f847f-353">若要重新執行工作流程，您必須執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="f847f-353">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="f847f-354">刪除 Hive 指令碼輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="f847f-354">Delete the Hive script output file.</span></span>
* <span data-ttu-id="f847f-355">刪除 log4jLogsCount 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="f847f-355">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="f847f-356">以下是您可使用的範例 Windows PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="f847f-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="f847f-357">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f847f-357">Next steps</span></span>
<span data-ttu-id="f847f-358">在本教學課程中，您已了解如何定義 Oozie 工作流程和 Oozie 協調器，以及如何使用 Azure PowerShell 來執行 Oozie 協調器工作。</span><span class="sxs-lookup"><span data-stu-id="f847f-358">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="f847f-359">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="f847f-359">To learn more, see the following articles:</span></span>

* <span data-ttu-id="f847f-360">[開始使用 HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f847f-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="f847f-361">[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="f847f-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="f847f-362">[使用 Azure PowerShell 管理 HDInsight][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="f847f-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="f847f-363">[將資料上傳至 HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="f847f-363">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="f847f-364">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="f847f-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="f847f-365">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f847f-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f847f-366">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f847f-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f847f-367">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="f847f-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

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
