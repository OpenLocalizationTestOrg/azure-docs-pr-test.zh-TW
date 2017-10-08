---
title: "aaaAccess Hadoop YARN 應用程式以程式設計方式-記錄 Azure |Microsoft 文件"
description: "在 HDInsight 中的 Hadoop 叢集上以程式設計方式存取應用程式記錄檔"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a><span data-ttu-id="9f4d3-103">存取以 Windows 為基礎之 HDInsight 上的 YARN 應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="9f4d3-103">Access YARN application logs on Windows-based HDInsight</span></span>
<span data-ttu-id="9f4d3-104">本主題說明如何 tooaccess hello 完 Azure HDInsight 中的 Windows 架構的 Hadoop 叢集的 YARN （尚未另一個資源交涉器） 應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="9f4d3-104">This topic explains how tooaccess hello logs for YARN (Yet Another Resource Negotiator) applications that have finished on a Windows-based Hadoop cluster in Azure HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f4d3-105">本文件中的 hello 資訊適用於僅 tooWindows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-105">hello information in this document applies only tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="9f4d3-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9f4d3-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="9f4d3-108">如需存取 Linux 之 HDInsight 叢集上 YARN 記錄檔的相關資訊，請參閱 [在 HDInsight 中的 Linux 之 Hadoop 上存取 YARN 應用程式記錄檔](hdinsight-hadoop-access-yarn-app-logs-linux.md)</span><span class="sxs-lookup"><span data-stu-id="9f4d3-108">For information on accessing YARN logs on Linux-based HDInsight clusters, see [Access YARN application logs on Linux-based Hadoop on HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md)</span></span>
>


### <a name="prerequisites"></a><span data-ttu-id="9f4d3-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="9f4d3-109">Prerequisites</span></span>
* <span data-ttu-id="9f4d3-110">Windows 型 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-110">A Windows-based HDInsight cluster.</span></span>  <span data-ttu-id="9f4d3-111">請參閱 [在 HDInsight 中建立 Windows 型 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-111">See [Create Windows-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="yarn-timeline-server"></a><span data-ttu-id="9f4d3-112">YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="9f4d3-112">YARN Timeline Server</span></span>
<span data-ttu-id="9f4d3-113">hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN 時間表伺服器</a>上完成的應用程式透過兩個不同的介面以及為特定架構應用程式資訊提供一般資訊。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-113">hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a> provides generic information on completed applications as well as framework-specific application information through two different interfaces.</span></span> <span data-ttu-id="9f4d3-114">具體而言：</span><span class="sxs-lookup"><span data-stu-id="9f4d3-114">Specifically:</span></span>

* <span data-ttu-id="9f4d3-115">儲存及擷取 HDInsight 叢集上泛型應用程式資訊的功能已在版本 3.1.1.374 或更新版本上啟用。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-115">Storage and retrieval of generic application information on HDInsight clusters has been enabled with version 3.1.1.374 or higher.</span></span>
* <span data-ttu-id="9f4d3-116">無法 HDInsight 叢集上目前可用的 hello 時間表伺服器 hello 架構特定應用程式資訊的元件。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-116">hello framework-specific application information component of hello Timeline Server is not currently available on HDInsight clusters.</span></span>

<span data-ttu-id="9f4d3-117">應用程式的一般資訊包含下列排序的資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f4d3-117">Generic information on applications includes hello following sorts of data:</span></span>

* <span data-ttu-id="9f4d3-118">hello 應用程式識別碼，應用程式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="9f4d3-118">hello application ID, a unique identifier of an application</span></span>
* <span data-ttu-id="9f4d3-119">啟動 hello 應用程式的 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="9f4d3-119">hello user who started hello application</span></span>
* <span data-ttu-id="9f4d3-120">資訊在嘗試進行 toocomplete hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="9f4d3-120">Information on attempts made toocomplete hello application</span></span>
* <span data-ttu-id="9f4d3-121">使用指定的應用程式的任何嘗試 hello 容器</span><span class="sxs-lookup"><span data-stu-id="9f4d3-121">hello containers used by any given application attempt</span></span>

<span data-ttu-id="9f4d3-122">在您的 HDInsight 叢集，此資訊將會儲存 hello 預設 Azure 儲存體帳戶的預設容器中的 Azure Resource Manager tooa 記錄存放區。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-122">On your HDInsight clusters, this information will be stored by Azure Resource Manager tooa history store in hello default container of your default Azure Storage account.</span></span> <span data-ttu-id="9f4d3-123">透過 REST API 即可抓取這項已完成之應用程式的相關泛型資料：</span><span class="sxs-lookup"><span data-stu-id="9f4d3-123">This generic data on completed applications can be retrieved through a REST API:</span></span>

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a><span data-ttu-id="9f4d3-124">YARN 應用程式和記錄檔</span><span class="sxs-lookup"><span data-stu-id="9f4d3-124">YARN applications and logs</span></span>
<span data-ttu-id="9f4d3-125">YARN 藉由將資源管理從應用程式排程/監視分離，支援多種程式設計模型 (MapReduce 為其中之一)。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-125">YARN supports multiple programming models (MapReduce being one of them) by decoupling resource management from application scheduling/monitoring.</span></span> <span data-ttu-id="9f4d3-126">這是透過全域 *ResourceManager* (RM)、每一背景工作節點 *ResourceManager* (NM) 及每一應用程式 *ResourceManager* (AM) 來達成。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-126">This is done through a global *ResourceManager* (RM), per-worker-node *NodeManagers* (NMs), and per-application *ApplicationMasters* (AMs).</span></span> <span data-ttu-id="9f4d3-127">hello AM 每個應用程式會交涉資源 （CPU、 記憶體、 磁碟、 網路） hello RM 中執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="9f4d3-127">hello per-application AM negotiates resources (CPU, memory, disk, network) for running your application with hello RM.</span></span> <span data-ttu-id="9f4d3-128">hello RM 搭配 NMs toogrant 做為被授與這些資源*容器*。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-128">hello RM works with NMs toogrant these resources, which are granted as *containers*.</span></span> <span data-ttu-id="9f4d3-129">hello AM 負責追蹤 hello RM hello 分派容器 tooit hello 進度</span><span class="sxs-lookup"><span data-stu-id="9f4d3-129">hello AM is responsible for tracking hello progress of hello containers assigned tooit by hello RM.</span></span> <span data-ttu-id="9f4d3-130">應用程式可能需要根據 hello 本質 hello 應用程式的許多容器。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-130">An application may require many containers depending on hello nature of hello application.</span></span>

<span data-ttu-id="9f4d3-131">此外，每個應用程式可能包含多個*應用程式嘗試*在 hello 是否存在的當機或 toohello 遺失 AM 之間的通訊中的順序 toofinish 和 RM</span><span class="sxs-lookup"><span data-stu-id="9f4d3-131">Furthermore, each application may consist of multiple *application attempts* in order toofinish in hello presence of crashes or due toohello loss of communication between an AM and an RM.</span></span> <span data-ttu-id="9f4d3-132">因此，容器會授與應用程式的 tooa 特定嘗試。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-132">Hence, containers are granted tooa specific attempt of an application.</span></span> <span data-ttu-id="9f4d3-133">某方面來說，容器會提供基本 YARN 應用程式所執行的工作單位的 hello 內容且完成 hello 內容的容器內的所有工作上都執行 hello 單一背景工作節點的 hello 配置容器。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-133">In a sense, a container provides hello context for basic unit of work performed by a YARN application, and all work that is done within hello context of a container is performed on hello single worker node on which hello container was allocated.</span></span> <span data-ttu-id="9f4d3-134">請參閱 [YARN 概念][YARN-concepts]，以取得進一步的參考資料。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-134">See [YARN Concepts][YARN-concepts] for further reference.</span></span>

<span data-ttu-id="9f4d3-135">應用程式記錄檔 （及相關聯的 hello 容器記錄） 在中不可或缺偵錯問題的 Hadoop 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-135">Application logs (and hello associated container logs) are critical in debugging problematic Hadoop applications.</span></span> <span data-ttu-id="9f4d3-136">YARN 所提供的不錯的架構，用於收集、 彙總，並儲存應用程式記錄檔以 hello[記錄彙總][ log-aggregation]功能。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-136">YARN provides a nice framework for collecting, aggregating, and storing application logs with hello [Log Aggregation][log-aggregation] feature.</span></span> <span data-ttu-id="9f4d3-137">hello 記錄彙總功能可讓存取的應用程式記錄檔更具決定性，因為它會彙總的背景工作節點上的所有容器的記錄檔並將它們儲存為一個彙總記錄檔每個背景工作節點 hello 預設檔案系統上，應用程式完成之後。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-137">hello Log Aggregation feature makes accessing application logs more deterministic, as it aggregates logs across all containers on a worker node and stores them as one aggregated log file per worker node on hello default file system after an application finishes.</span></span> <span data-ttu-id="9f4d3-138">您的應用程式可能會使用數百或數千個容器，但在單一的背景工作節點上執行的所有容器的記錄檔就會永遠彙總的 tooa 單一檔案，導致每個應用程式所使用的背景工作節點建立一個記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-138">Your application may use hundreds or thousands of containers, but logs for all containers run on a single worker node will always be aggregated tooa single file, resulting in one log file per worker node used by your application.</span></span> <span data-ttu-id="9f4d3-139">HDInsight 叢集上的預設會啟用記錄檔彙總 (3.0 版和更新版本)，並彙總的記錄檔可以找到您的叢集，在下列位置的 hello hello 預設容器中：</span><span class="sxs-lookup"><span data-stu-id="9f4d3-139">Log Aggregation is enabled by default on HDInsight clusters (version 3.0 and above), and aggregated logs can be found in hello default container of your cluster at hello following location:</span></span>

    wasb:///app-logs/<user>/logs/<applicationId>

<span data-ttu-id="9f4d3-140">在該位置，*使用者*hello hello 啟動 hello 應用程式，使用者名稱和*applicationId* hello YARN RM 指派為 hello 的應用程式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="9f4d3-140">In that location, *user* is hello name of hello user who started hello application, and *applicationId* is hello unique identifier of an application as assigned by hello YARN RM.</span></span>

<span data-ttu-id="9f4d3-141">hello 彙總的記錄檔並未直接讀取，它們會以撰寫[TFile][T-file]，[二進位格式][ binary-format]容器以編製索引。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-141">hello aggregated logs are not directly readable, as they are written in a [TFile][T-file], [binary format][binary-format] indexed by container.</span></span> <span data-ttu-id="9f4d3-142">YARN 提供 CLI 工具 toodump 這些記錄檔以純文字的應用程式或感興趣的容器。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-142">YARN provides CLI tools toodump these logs as plain text for applications or containers of interest.</span></span> <span data-ttu-id="9f4d3-143">您可以執行其中一種 hello 之後直接在 hello 叢集節點上的 YARN 命令 （之後透過 RDP 連線 tooit），以純文字檢視這些記錄檔：</span><span class="sxs-lookup"><span data-stu-id="9f4d3-143">You can view these logs as plain text by running one of hello following YARN commands directly on hello cluster nodes (after connecting tooit through RDP):</span></span>

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a><span data-ttu-id="9f4d3-144">YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="9f4d3-144">YARN ResourceManager UI</span></span>
<span data-ttu-id="9f4d3-145">hello YARN ResourceManager UI hello 叢集叢集前端節點上執行，而且可以存取透過 Azure 入口網站的儀表板 hello:</span><span class="sxs-lookup"><span data-stu-id="9f4d3-145">hello YARN ResourceManager UI runs on hello cluster headnode, and can be accessed through hello Azure portal dashboard:</span></span>

1. <span data-ttu-id="9f4d3-146">登入太[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-146">Sign in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9f4d3-147">在 hello 左窗格中，按一下 **瀏覽**，按一下  **HDInsight 叢集**，按一下您想 tooaccess hello YARN 應用程式記錄檔的 windows 叢集。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-147">On hello left menu, click **Browse**, click **HDInsight Clusters**, click a Windows-based cluster that you want tooaccess hello YARN application logs.</span></span>
3. <span data-ttu-id="9f4d3-148">在 hello 上方功能表中，按一下 **儀表板**。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-148">On hello top menu, click **Dashboard**.</span></span> <span data-ttu-id="9f4d3-149">您會看到有頁面在新的瀏覽器索引標籤上開啟，其名稱為 **HDInsight 查詢主控台**。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-149">You will see a page opened on a new browser tab called **HDInsight Query Console**.</span></span>
4. <span data-ttu-id="9f4d3-150">在 [HDInsight 查詢主控台] 上，按一下 [Yarn UI]。</span><span class="sxs-lookup"><span data-stu-id="9f4d3-150">From **HDInsight Query Console**, click **Yarn UI**.</span></span>

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
