---
title: "存取以 Linux 為基礎之 HDInsight 上的 Hadoop YARN 應用程式記錄檔 - Azure | Microsoft Docs"
description: "了解如何使用命令列和網頁瀏覽器存取以 Linux 為基礎之 HDInsight (Hadoop) 叢集上的 YARN 應用程式記錄檔。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: fbbbddc47f24a46eac9bc64d4420ee8429ed4ad1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a><span data-ttu-id="e8b70-103">存取以 Linux 為基礎之 HDInsight 上的 YARN 應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="e8b70-103">Access YARN application logs on Linux-based HDInsight</span></span>

<span data-ttu-id="e8b70-104">了解如何存取 Azure HDInsight 的 Hadoop 叢集上之 YARN (Yet Another Resource Negotiator) 應用程式的記錄。</span><span class="sxs-lookup"><span data-stu-id="e8b70-104">Learn how to access the logs for YARN (Yet Another Resource Negotiator) applications on a Hadoop cluster in Azure HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8b70-105">此文件中的步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e8b70-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="e8b70-106">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="e8b70-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e8b70-107">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="e8b70-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="e8b70-108"><a name="YARNTimelineServer"></a>YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="e8b70-108"><a name="YARNTimelineServer"></a>YARN Timeline Server</span></span>

<span data-ttu-id="e8b70-109">[YARN Timeline Server (英文)](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) 透過兩個不同的介面，提供完整應用程式的一般資訊，以及架構的特定應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="e8b70-109">The [YARN Timeline Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) provides generic information on completed applications and framework-specific application information through two different interfaces.</span></span> <span data-ttu-id="e8b70-110">具體而言：</span><span class="sxs-lookup"><span data-stu-id="e8b70-110">Specifically:</span></span>

* <span data-ttu-id="e8b70-111">儲存及擷取 HDInsight 叢集上泛型應用程式資訊的功能已在版本 3.1.1.374 或更新版本上啟用。</span><span class="sxs-lookup"><span data-stu-id="e8b70-111">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span></span>
* <span data-ttu-id="e8b70-112">Timeline Server 的架構特定應用程式資訊元件目前在 HDInsight 叢集上並未提供。</span><span class="sxs-lookup"><span data-stu-id="e8b70-112">The framework-specific application information component of the Timeline Server is not currently available on HDInsight clusters.</span></span>

<span data-ttu-id="e8b70-113">應用程式的一般資訊包括下列類型的資料：</span><span class="sxs-lookup"><span data-stu-id="e8b70-113">Generic information on applications includes the following type of data:</span></span>

* <span data-ttu-id="e8b70-114">應用程式識別碼，應用程式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e8b70-114">The application ID, a unique identifier of an application</span></span>
* <span data-ttu-id="e8b70-115">啟動應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="e8b70-115">The user who started the application</span></span>
* <span data-ttu-id="e8b70-116">為完成應用程式而進行之嘗試的相關資訊</span><span class="sxs-lookup"><span data-stu-id="e8b70-116">Information on attempts made to complete the application</span></span>
* <span data-ttu-id="e8b70-117">任何指定之應用程式嘗試所使用的容器</span><span class="sxs-lookup"><span data-stu-id="e8b70-117">The containers used by any given application attempt</span></span>

## <span data-ttu-id="e8b70-118"><a name="YARNAppsAndLogs"></a>YARN 應用程式和記錄檔</span><span class="sxs-lookup"><span data-stu-id="e8b70-118"><a name="YARNAppsAndLogs"></a>YARN applications and logs</span></span>

<span data-ttu-id="e8b70-119">YARN 藉由將資源管理從應用程式排程/監視分離，支援多種程式設計模型 (MapReduce 為其中之一)。</span><span class="sxs-lookup"><span data-stu-id="e8b70-119">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span></span> <span data-ttu-id="e8b70-120">YARN 使用全域 *ResourceManager* (RM)、每一背景工作節點 *ResourceManager* (NM) 及每一應用程式 *ResourceManager* (AM)。</span><span class="sxs-lookup"><span data-stu-id="e8b70-120">YARN uses a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span></span> <span data-ttu-id="e8b70-121">每一應用程式 AM 會與 RM 交涉用來執行您應用程式的資源 (CPU、記憶體、磁碟、網路)。</span><span class="sxs-lookup"><span data-stu-id="e8b70-121">The per-application AM negotiates resources (CPU, memory, disk, network) for running your application with the RM.</span></span> <span data-ttu-id="e8b70-122">RM 會與 NM 合作來授與這些資源 (以「 *容器*」的形式授與)。</span><span class="sxs-lookup"><span data-stu-id="e8b70-122">The RM works with NMs to grant these resources, which are granted as *containers*.</span></span> <span data-ttu-id="e8b70-123">AM 則是負責追蹤 RM 指派給它之容器的進度。</span><span class="sxs-lookup"><span data-stu-id="e8b70-123">The AM is responsible for tracking the progress of the containers assigned to it by the RM.</span></span> <span data-ttu-id="e8b70-124">視應用程式的本質而定，一個應用程式可能會需要許多容器。</span><span class="sxs-lookup"><span data-stu-id="e8b70-124">An application may require many containers depending on the nature of the application.</span></span>

<span data-ttu-id="e8b70-125">每個應用程式都可能包含多個「應用程式嘗試」。</span><span class="sxs-lookup"><span data-stu-id="e8b70-125">Each application may consist of multiple *application attempts*.</span></span> <span data-ttu-id="e8b70-126">如果應用程式失敗，系統可能會以新的嘗試來重試它。</span><span class="sxs-lookup"><span data-stu-id="e8b70-126">If an application fails, it may be retried as a new attempt.</span></span> <span data-ttu-id="e8b70-127">每個嘗試都在容器中執行。</span><span class="sxs-lookup"><span data-stu-id="e8b70-127">Each attempt runs in a container.</span></span> <span data-ttu-id="e8b70-128">從某方面來說，容器提供由 YARN 應用程式所執行之作業的基本單位內容。</span><span class="sxs-lookup"><span data-stu-id="e8b70-128">In a sense, a container provides the context for basic unit of work performed by a YARN application.</span></span> <span data-ttu-id="e8b70-129">所有於容器內容之內所執行的作業，都會在容器所配置的單一背景工作節點上執行。</span><span class="sxs-lookup"><span data-stu-id="e8b70-129">All work that is done within the context of a container is performed on the single worker node on which the container was allocated.</span></span> <span data-ttu-id="e8b70-130">請參閱 [YARN 概念][YARN-concepts]，以取得進一步的參考資料。</span><span class="sxs-lookup"><span data-stu-id="e8b70-130">See [YARN Concepts][YARN-concepts] for further reference.</span></span>

<span data-ttu-id="e8b70-131">應用程式記錄檔 (和關聯的容器記錄檔) 在對有問題的 Hadoop 應用程式進行偵錯上相當重要。</span><span class="sxs-lookup"><span data-stu-id="e8b70-131">Application logs (and the associated container logs) are critical in debugging problematic Hadoop applications.</span></span> <span data-ttu-id="e8b70-132">YARN 以 [記錄檔彙總][log-aggregation] 功能提供一個良好的架構，以收集、彙總及儲存應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e8b70-132">YARN provides a nice framework for collecting, aggregating, and storing application logs with the [Log Aggregation][log-aggregation] feature.</span></span> <span data-ttu-id="e8b70-133">「記錄檔彙總」功能可使存取應用程式記錄更具確定性。</span><span class="sxs-lookup"><span data-stu-id="e8b70-133">The Log Aggregation feature makes accessing application logs more deterministic.</span></span> <span data-ttu-id="e8b70-134">它能彙總背景工作節點上所有容器的記錄檔，並將它們依每個背景工作節點儲存成單一彙總記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e8b70-134">It aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node.</span></span> <span data-ttu-id="e8b70-135">在應用程式完成之後，記錄檔會儲存在預設檔案系統上。</span><span class="sxs-lookup"><span data-stu-id="e8b70-135">The log is stored on the default file system after an application finishes.</span></span> <span data-ttu-id="e8b70-136">您的應用程式可能使用數百或數千個容器，但在單一背景工作節點上執行之所有容器的記錄一律彙總成單一檔案。</span><span class="sxs-lookup"><span data-stu-id="e8b70-136">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node are always aggregated to a single file.</span></span> <span data-ttu-id="e8b70-137">因此，應用程式使用的每一背景工作節點只會有 1 個記錄。</span><span class="sxs-lookup"><span data-stu-id="e8b70-137">So there is only 1 log per worker node used by your application.</span></span> <span data-ttu-id="e8b70-138">根據預設，HDInsight 叢集 3.0 版和更新版本上會啟用記錄彙總。</span><span class="sxs-lookup"><span data-stu-id="e8b70-138">Log Aggregation is enabled by default on HDInsight clusters version 3.0 and above.</span></span> <span data-ttu-id="e8b70-139">彙總記錄位於叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="e8b70-139">Aggregated logs are located in default storage for the cluster.</span></span> <span data-ttu-id="e8b70-140">下列路徑是記錄的 HDFS 路徑︰</span><span class="sxs-lookup"><span data-stu-id="e8b70-140">The following path is the HDFS path to the logs:</span></span>

    /app-logs/<user>/logs/<applicationId>

<span data-ttu-id="e8b70-141">在路徑中，`user` 是啟動應用程式的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e8b70-141">In the path, `user` is the name of the user who started the application.</span></span> <span data-ttu-id="e8b70-142">`applicationId` 是 YARN RM 指派給應用程式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e8b70-142">The `applicationId` is the unique identifier assigned to an application by the YARN RM.</span></span>

<span data-ttu-id="e8b70-143">您無法直接閱讀彙總的記錄檔，因為它們是以 [TFile][T-file]、由容器編製索引的 [二進位格式][binary-format] 撰寫。</span><span class="sxs-lookup"><span data-stu-id="e8b70-143">The aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span></span> <span data-ttu-id="e8b70-144">對於您感興趣的應用程式或容器，請使用 YARN ResourceManager 記錄或 CLI 工具來檢視純文字記錄。</span><span class="sxs-lookup"><span data-stu-id="e8b70-144">Use the YARN ResourceManager logs or CLI tools to view these logs as plain text for applications or containers of interest.</span></span>

## <a name="yarn-cli-tools"></a><span data-ttu-id="e8b70-145">YARN CLI 工具</span><span class="sxs-lookup"><span data-stu-id="e8b70-145">YARN CLI tools</span></span>

<span data-ttu-id="e8b70-146">若要使用 YARN CLI 工具，您必須先使用 SSH 連接到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e8b70-146">To use the YARN CLI tools, you must first connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="e8b70-147">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="e8b70-147">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="e8b70-148">您可以執行下列其中一個命令，以檢視這些純文字記錄：</span><span class="sxs-lookup"><span data-stu-id="e8b70-148">You can view these logs as plain text by running one of the following commands:</span></span>

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

<span data-ttu-id="e8b70-149">執行這些命令時，請指定 &lt;applicationId>、&lt;user-who-started-the-application>、&lt;containerId> 及 &lt;worker-node-address> 資訊。</span><span class="sxs-lookup"><span data-stu-id="e8b70-149">Specify the &lt;applicationId>, &lt;user-who-started-the-application>, &lt;containerId>, and &lt;worker-node-address> information when running these commands.</span></span>

## <a name="yarn-resourcemanager-ui"></a><span data-ttu-id="e8b70-150">YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="e8b70-150">YARN ResourceManager UI</span></span>

<span data-ttu-id="e8b70-151">YARN ResourceManager UI 是在叢集前端節點上執行。</span><span class="sxs-lookup"><span data-stu-id="e8b70-151">The YARN ResourceManager UI runs on the cluster headnode.</span></span> <span data-ttu-id="e8b70-152">可透過 Ambari Web UI 存取。</span><span class="sxs-lookup"><span data-stu-id="e8b70-152">It is accessed through the Ambari web UI.</span></span> <span data-ttu-id="e8b70-153">請使用下列步驟來檢視 YARN 記錄：</span><span class="sxs-lookup"><span data-stu-id="e8b70-153">Use the following steps to view the YARN logs:</span></span>

1. <span data-ttu-id="e8b70-154">在網頁瀏覽器中，瀏覽至 https://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="e8b70-154">In your web browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="e8b70-155">將 CLUSTERNAME 取代為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="e8b70-155">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="e8b70-156">從左邊的服務清單中選取 [YARN] 。</span><span class="sxs-lookup"><span data-stu-id="e8b70-156">From the list of services on the left, select **YARN**.</span></span>

    ![選取的 Yarn 服務](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. <span data-ttu-id="e8b70-158">在 [快速連結] 下拉式清單中，選取其中一個叢集前端節點，然後選取 [ResourceManager 記錄]。</span><span class="sxs-lookup"><span data-stu-id="e8b70-158">From the **Quick Links** dropdown, select one of the cluster head nodes and then select **ResourceManager Log**.</span></span>

    ![Yarn 快速連結](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    <span data-ttu-id="e8b70-160">您會看到一份 YARN 記錄檔的連結清單。</span><span class="sxs-lookup"><span data-stu-id="e8b70-160">You are presented with a list of links to YARN logs.</span></span>

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
