---
title: "aaaAccess Hadoop YARN 應用程式登入以 Linux 為基礎的 HDInsight 的 Azure |Microsoft 文件"
description: "了解 tooaccess YARN 應用程式登入使用命令列 hello 和網頁瀏覽器以 Linux 為基礎的 HDInsight (Hadoop) 叢集的方式。"
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
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a><span data-ttu-id="9cf2e-103">存取以 Linux 為基礎之 HDInsight 上的 YARN 應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="9cf2e-103">Access YARN application logs on Linux-based HDInsight</span></span>

<span data-ttu-id="9cf2e-104">了解如何 tooaccess hello YARN （尚未另一個資源交涉器） 在 Azure HDInsight Hadoop 叢集上的應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-104">Learn how tooaccess hello logs for YARN (Yet Another Resource Negotiator) applications on a Hadoop cluster in Azure HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cf2e-105">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="9cf2e-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9cf2e-107">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="9cf2e-108"><a name="YARNTimelineServer"></a>YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="9cf2e-108"><a name="YARNTimelineServer"></a>YARN Timeline Server</span></span>

<span data-ttu-id="9cf2e-109">hello [YARN 時間表伺服器](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html)完成的應用程式與透過兩個不同介面的架構特定應用程式資訊提供一般資訊。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-109">hello [YARN Timeline Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) provides generic information on completed applications and framework-specific application information through two different interfaces.</span></span> <span data-ttu-id="9cf2e-110">具體而言：</span><span class="sxs-lookup"><span data-stu-id="9cf2e-110">Specifically:</span></span>

* <span data-ttu-id="9cf2e-111">儲存及擷取 HDInsight 叢集上泛型應用程式資訊的功能已在版本 3.1.1.374 或更新版本上啟用。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-111">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span></span>
* <span data-ttu-id="9cf2e-112">無法 HDInsight 叢集上目前可用的 hello 時間表伺服器 hello 架構特定應用程式資訊的元件。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-112">hello framework-specific application information component of hello Timeline Server is not currently available on HDInsight clusters.</span></span>

<span data-ttu-id="9cf2e-113">應用程式的一般資訊包含下列資料類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="9cf2e-113">Generic information on applications includes hello following type of data:</span></span>

* <span data-ttu-id="9cf2e-114">hello 應用程式識別碼，應用程式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="9cf2e-114">hello application ID, a unique identifier of an application</span></span>
* <span data-ttu-id="9cf2e-115">啟動 hello 應用程式的 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="9cf2e-115">hello user who started hello application</span></span>
* <span data-ttu-id="9cf2e-116">資訊在嘗試進行 toocomplete hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="9cf2e-116">Information on attempts made toocomplete hello application</span></span>
* <span data-ttu-id="9cf2e-117">使用指定的應用程式的任何嘗試 hello 容器</span><span class="sxs-lookup"><span data-stu-id="9cf2e-117">hello containers used by any given application attempt</span></span>

## <span data-ttu-id="9cf2e-118"><a name="YARNAppsAndLogs"></a>YARN 應用程式和記錄檔</span><span class="sxs-lookup"><span data-stu-id="9cf2e-118"><a name="YARNAppsAndLogs"></a>YARN applications and logs</span></span>

<span data-ttu-id="9cf2e-119">YARN 藉由將資源管理從應用程式排程/監視分離，支援多種程式設計模型 (MapReduce 為其中之一)。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-119">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span></span> <span data-ttu-id="9cf2e-120">YARN 使用全域 *ResourceManager* (RM)、每一背景工作節點 *ResourceManager* (NM) 及每一應用程式 *ResourceManager* (AM)。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-120">YARN uses a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span></span> <span data-ttu-id="9cf2e-121">hello AM 每個應用程式會交涉資源 （CPU、 記憶體、 磁碟、 網路） hello RM 中執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="9cf2e-121">hello per-application AM negotiates resources (CPU, memory, disk, network) for running your application with hello RM.</span></span> <span data-ttu-id="9cf2e-122">hello RM 搭配 NMs toogrant 做為被授與這些資源*容器*。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-122">hello RM works with NMs toogrant these resources, which are granted as *containers*.</span></span> <span data-ttu-id="9cf2e-123">hello AM 負責追蹤 hello RM hello 分派容器 tooit hello 進度</span><span class="sxs-lookup"><span data-stu-id="9cf2e-123">hello AM is responsible for tracking hello progress of hello containers assigned tooit by hello RM.</span></span> <span data-ttu-id="9cf2e-124">應用程式可能需要根據 hello 本質 hello 應用程式的許多容器。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-124">An application may require many containers depending on hello nature of hello application.</span></span>

<span data-ttu-id="9cf2e-125">每個應用程式都可能包含多個「應用程式嘗試」。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-125">Each application may consist of multiple *application attempts*.</span></span> <span data-ttu-id="9cf2e-126">如果應用程式失敗，系統可能會以新的嘗試來重試它。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-126">If an application fails, it may be retried as a new attempt.</span></span> <span data-ttu-id="9cf2e-127">每個嘗試都在容器中執行。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-127">Each attempt runs in a container.</span></span> <span data-ttu-id="9cf2e-128">某方面來說，容器會提供基本的 YARN 應用程式所執行的工作單位的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-128">In a sense, a container provides hello context for basic unit of work performed by a YARN application.</span></span> <span data-ttu-id="9cf2e-129">完成 hello 內容的容器內的所有工作是在哪一個 hello 配置容器的 hello 單一背景工作節點上都執行。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-129">All work that is done within hello context of a container is performed on hello single worker node on which hello container was allocated.</span></span> <span data-ttu-id="9cf2e-130">請參閱 [YARN 概念][YARN-concepts]，以取得進一步的參考資料。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-130">See [YARN Concepts][YARN-concepts] for further reference.</span></span>

<span data-ttu-id="9cf2e-131">應用程式記錄檔 （及相關聯的 hello 容器記錄） 在中不可或缺偵錯問題的 Hadoop 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-131">Application logs (and hello associated container logs) are critical in debugging problematic Hadoop applications.</span></span> <span data-ttu-id="9cf2e-132">YARN 所提供的不錯的架構，用於收集、 彙總，並儲存應用程式記錄檔以 hello[記錄彙總][ log-aggregation]功能。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-132">YARN provides a nice framework for collecting, aggregating, and storing application logs with hello [Log Aggregation][log-aggregation] feature.</span></span> <span data-ttu-id="9cf2e-133">hello 記錄彙總功能可讓您更具決定性存取應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-133">hello Log Aggregation feature makes accessing application logs more deterministic.</span></span> <span data-ttu-id="9cf2e-134">它能彙總背景工作節點上所有容器的記錄檔，並將它們依每個背景工作節點儲存成單一彙總記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-134">It aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node.</span></span> <span data-ttu-id="9cf2e-135">hello 記錄會儲存在 hello 預設的檔案系統上，應用程式完成之後。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-135">hello log is stored on hello default file system after an application finishes.</span></span> <span data-ttu-id="9cf2e-136">您的應用程式可能會使用數百或數千個容器，但記錄檔的單一工作者節點上執行的所有容器一律彙總的 tooa 單一檔案。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-136">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node are always aggregated tooa single file.</span></span> <span data-ttu-id="9cf2e-137">因此，應用程式使用的每一背景工作節點只會有 1 個記錄。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-137">So there is only 1 log per worker node used by your application.</span></span> <span data-ttu-id="9cf2e-138">根據預設，HDInsight 叢集 3.0 版和更新版本上會啟用記錄彙總。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-138">Log Aggregation is enabled by default on HDInsight clusters version 3.0 and above.</span></span> <span data-ttu-id="9cf2e-139">彙總的記錄檔位於預設儲存體 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-139">Aggregated logs are located in default storage for hello cluster.</span></span> <span data-ttu-id="9cf2e-140">下列路徑的 hello 是 hello HDFS 路徑 toohello 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="9cf2e-140">hello following path is hello HDFS path toohello logs:</span></span>

    /app-logs/<user>/logs/<applicationId>

<span data-ttu-id="9cf2e-141">在 hello 路徑`user`hello 啟動 hello 應用程式的 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-141">In hello path, `user` is hello name of hello user who started hello application.</span></span> <span data-ttu-id="9cf2e-142">hello`applicationId`是 hello hello YARN RM 所指派的唯一識別碼 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="9cf2e-142">hello `applicationId` is hello unique identifier assigned tooan application by hello YARN RM.</span></span>

<span data-ttu-id="9cf2e-143">hello 彙總的記錄檔並未直接讀取，它們會以撰寫[TFile][T-file]，[二進位格式][ binary-format]容器以編製索引。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-143">hello aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span></span> <span data-ttu-id="9cf2e-144">使用的 hello YARN ResourceManager 記錄或 CLI 工具 tooview 這些記錄檔以純文字的應用程式或感興趣的容器。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-144">Use hello YARN ResourceManager logs or CLI tools tooview these logs as plain text for applications or containers of interest.</span></span>

## <a name="yarn-cli-tools"></a><span data-ttu-id="9cf2e-145">YARN CLI 工具</span><span class="sxs-lookup"><span data-stu-id="9cf2e-145">YARN CLI tools</span></span>

<span data-ttu-id="9cf2e-146">toouse hello YARN CLI 工具 中，您必須先連接使用 SSH toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-146">toouse hello YARN CLI tools, you must first connect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="9cf2e-147">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-147">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="9cf2e-148">您可以執行其中一種 hello 下列命令，以純文字檢視這些記錄檔：</span><span class="sxs-lookup"><span data-stu-id="9cf2e-148">You can view these logs as plain text by running one of hello following commands:</span></span>

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

<span data-ttu-id="9cf2e-149">指定 hello &lt;applicationId >，&lt;使用者-使用者-啟動-應用程式 >， &lt;containerId >，並&lt;背景工作節點位址 > 時執行這些命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-149">Specify hello &lt;applicationId>, &lt;user-who-started-the-application>, &lt;containerId>, and &lt;worker-node-address> information when running these commands.</span></span>

## <a name="yarn-resourcemanager-ui"></a><span data-ttu-id="9cf2e-150">YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="9cf2e-150">YARN ResourceManager UI</span></span>

<span data-ttu-id="9cf2e-151">hello YARN ResourceManager UI 會 hello 叢集前端節點上執行。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-151">hello YARN ResourceManager UI runs on hello cluster headnode.</span></span> <span data-ttu-id="9cf2e-152">它是透過 hello Ambari web UI 存取。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-152">It is accessed through hello Ambari web UI.</span></span> <span data-ttu-id="9cf2e-153">使用下列步驟 tooview hello YARN 的 hello 記錄：</span><span class="sxs-lookup"><span data-stu-id="9cf2e-153">Use hello following steps tooview hello YARN logs:</span></span>

1. <span data-ttu-id="9cf2e-154">在網頁瀏覽器，瀏覽 toohttps://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-154">In your web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="9cf2e-155">CLUSTERNAME 取代 hello 的 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-155">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="9cf2e-156">從 hello hello 左側的服務清單，選取**YARN**。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-156">From hello list of services on hello left, select **YARN**.</span></span>

    ![選取的 Yarn 服務](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. <span data-ttu-id="9cf2e-158">從 hello**快速連結**下拉式清單中，選取一個 hello 叢集前端節點，然後選取**ResourceManager 記錄**。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-158">From hello **Quick Links** dropdown, select one of hello cluster head nodes and then select **ResourceManager Log**.</span></span>

    ![Yarn 快速連結](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    <span data-ttu-id="9cf2e-160">您會看到一份連結 tooYARN 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9cf2e-160">You are presented with a list of links tooYARN logs.</span></span>

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
