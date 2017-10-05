---
title: "使用 Ambari Web UI 監視和管理 Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Ambari 來監視和管理以 Linux 為基礎的 HDInsight 叢集。 在本文件中，您會學習如何使用 HDInsight 叢集隨附的 Ambari Web UI。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: dc0f9ff030f70985dad0f3b74ba0ee3dda1d9f4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-web-ui"></a><span data-ttu-id="dcbe5-104">使用 Ambari Web UI 管理 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dcbe5-104">Manage HDInsight clusters by using the Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="dcbe5-105">Apache Ambari 提供容易使用的 Web UI 和 REST API，可簡化 Hadoop 叢集的管理和監視。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="dcbe5-106">以 Linux 為基礎的 HDInsight 叢集上有 Ambari，用來監視叢集並進行組態變更。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span></span>

<span data-ttu-id="dcbe5-107">在本文件中，您會學習如何搭配使用 Ambari Web UI 和 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="dcbe5-108"><a id="whatis"></a>什麼是 Ambari？</span><span class="sxs-lookup"><span data-stu-id="dcbe5-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="dcbe5-109">[Apache Ambari](http://ambari.apache.org) 提供方便使用的 Web UI，簡化 Hadoop 管理。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="dcbe5-110">您可以使用 Ambari 建立、管理及監視 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="dcbe5-111">開發人員可以使用 [Ambari REST API](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)將這些功能整合到應用程式。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="dcbe5-112">使用 Linux 作業系統的 HDInsight 叢集預設會提供 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-112">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcbe5-113">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-113">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dcbe5-114">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="dcbe5-115">連線能力</span><span class="sxs-lookup"><span data-stu-id="dcbe5-115">Connectivity</span></span>

<span data-ttu-id="dcbe5-116">Ambari Web UI 位在您的 HDInsight 叢集的 HTTPS://CLUSTERNAME.azurehdidnsight.net，其中 **CLUSTERNAME** 是您的叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-116">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcbe5-117">連線到 HDInsight 上的 Ambari 需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-117">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="dcbe5-118">當系統提示要驗證時，請使用您在叢集建立時所提供的系統管理帳戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-118">When prompted for authentication, use the admin account name and password you provided when the cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="dcbe5-119">SSH 通道 (Proxy)</span><span class="sxs-lookup"><span data-stu-id="dcbe5-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="dcbe5-120">雖然您可直接透過網際網路存取叢集適用的 Ambari，但 Ambari Web UI 中的一些連結 (例如 JobTracker 的連結) 並不會在網際網路上公開。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-120">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker) are not exposed on the internet.</span></span> <span data-ttu-id="dcbe5-121">若要存取這些服務，您必須建立 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-121">To access these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="dcbe5-122">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="dcbe5-123">Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="dcbe5-123">Ambari Web UI</span></span>

<span data-ttu-id="dcbe5-124">連線到 Ambari Web UI 時，系統會提示您通過頁面驗證。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-124">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span></span> <span data-ttu-id="dcbe5-125">使用您在叢集建立期間使用的叢集管理使用者 (預設值是 Admin) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-125">Use the cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="dcbe5-126">當頁面開啟時，請注意頂端的資訊列。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-126">When the page opens, note the bar at the top.</span></span> <span data-ttu-id="dcbe5-127">此列包含下列資訊和控制項：</span><span class="sxs-lookup"><span data-stu-id="dcbe5-127">This bar contains the following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="dcbe5-129">**Ambari 標誌** - 開啟儀表板，以供用來監視叢集。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-129">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span></span>

* <span data-ttu-id="dcbe5-130">**叢集名稱 # 項作業** - 顯示進行中的 Ambari 作業數目。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-130">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span></span> <span data-ttu-id="dcbe5-131">選取叢集名稱或 [# 項作業] 會顯示背景作業清單。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-131">Selecting the cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="dcbe5-132">**# 個警示** - 顯示叢集的警告或重要警示 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-132">**# alerts** - Displays warnings or critical alerts, if any, for the cluster.</span></span>

* <span data-ttu-id="dcbe5-133">**儀表板** - 顯示儀表板。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-133">**Dashboard** - Displays the dashboard.</span></span>

* <span data-ttu-id="dcbe5-134">**服務** - 叢集中之服務的資訊和組態設定。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-134">**Services** - Information and configuration settings for the services in the cluster.</span></span>

* <span data-ttu-id="dcbe5-135">**主機** - 叢集中之節點的資訊和組態設定。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-135">**Hosts** - Information and configuration settings for the nodes in the cluster.</span></span>

* <span data-ttu-id="dcbe5-136">**警示** - 資訊、警告和重要警示的記錄。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="dcbe5-137">**系統管理員** - 已安裝於叢集的軟體堆疊/服務、服務帳戶資訊及 Kerberos 安全性。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-137">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="dcbe5-138">**系統管理員按鈕** - Ambari 管理、使用者設定和登出。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="dcbe5-139">監視</span><span class="sxs-lookup"><span data-stu-id="dcbe5-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="dcbe5-140">Alerts</span><span class="sxs-lookup"><span data-stu-id="dcbe5-140">Alerts</span></span>

<span data-ttu-id="dcbe5-141">下列清單包含 Ambari 常用的警示狀態︰</span><span class="sxs-lookup"><span data-stu-id="dcbe5-141">The following list contains the common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="dcbe5-142">**確定**</span><span class="sxs-lookup"><span data-stu-id="dcbe5-142">**OK**</span></span>
* <span data-ttu-id="dcbe5-143">**警告**</span><span class="sxs-lookup"><span data-stu-id="dcbe5-143">**Warning**</span></span>
* <span data-ttu-id="dcbe5-144">**重要**</span><span class="sxs-lookup"><span data-stu-id="dcbe5-144">**CRITICAL**</span></span>
* <span data-ttu-id="dcbe5-145">**未知**</span><span class="sxs-lookup"><span data-stu-id="dcbe5-145">**UNKNOWN**</span></span>

<span data-ttu-id="dcbe5-146">[確定] 以外的警示會導致頁面頂端出現 [# 個警示] 項目，以顯示警示數目。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-146">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span></span> <span data-ttu-id="dcbe5-147">選取此項目會顯示警示及其狀態。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-147">Selecting this entry displays the alerts and their status.</span></span>

<span data-ttu-id="dcbe5-148">警示分成數個預設群組，您可以從 [ **警示** ] 頁面進行檢視。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-148">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span></span>

![警示頁面](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="dcbe5-150">您可以使用 [動作] 功能表並選取 [管理警示群組] 來管理這些群組。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-150">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![管理警示群組對話方塊](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="dcbe5-152">您也可以管理警示方法，並從 [動作] 功能表中選取 [管理警示通知] 來建立警示通知。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-152">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="dcbe5-153">系統會顯示任何目前的通知。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-153">Any current notifications are displayed.</span></span> <span data-ttu-id="dcbe5-154">您也可以從這裡建立通知。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-154">You can also create notifications from here.</span></span> <span data-ttu-id="dcbe5-155">在發生特定警示/嚴重性組合時，便可透過**電子郵件**或 **SNMP** 傳送通知。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="dcbe5-156">例如，您可以在 [YARN 預設] 群組中的任何警示設為 [重要] 時傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-156">For example, you can send an email message when any of the alerts in the **YARN Default** group is set to **Critical**.</span></span>

![建立警示對話方塊](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="dcbe5-158">最後，從 [動作] 功能表選取 [管理警示設定] 可讓您設定必須發生幾次警示才會傳送通知。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-158">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you to set the number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="dcbe5-159">這項設定可以用來防止暫時性錯誤的通知。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-159">This setting can be used to prevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="dcbe5-160">叢集</span><span class="sxs-lookup"><span data-stu-id="dcbe5-160">Cluster</span></span>

<span data-ttu-id="dcbe5-161">儀表板的 [ **度量** ] 索引標籤包含一系列的 Widget，可讓您一目了然地輕鬆監視叢集的狀態。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-161">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span></span> <span data-ttu-id="dcbe5-162">[ **CPU 使用量**] 等數個 Widget 可在點按後提供其他資訊。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![儀表板與度量](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="dcbe5-164">[ **熱圖** ] 索引標籤會以綠色到紅色的彩色熱圖顯示度量。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-164">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span></span>

![儀表板與熱圖](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="dcbe5-166">如需有關叢集中節點的詳細資訊，請選取 [主機]。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-166">For more information on the nodes within the cluster, select **Hosts**.</span></span> <span data-ttu-id="dcbe5-167">然後選取您感興趣的特定節點。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-167">Then select the specific node you are interested in.</span></span>

![主機詳細資料](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="dcbe5-169">服務</span><span class="sxs-lookup"><span data-stu-id="dcbe5-169">Services</span></span>

<span data-ttu-id="dcbe5-170">儀表板上的 [ **服務** ] 提要欄位可讓您快速了解叢集上執行之服務的狀態。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-170">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span></span> <span data-ttu-id="dcbe5-171">各種圖示用來指出狀態或應採取的動作。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-171">Various icons are used to indicate status or actions that should be taken.</span></span> <span data-ttu-id="dcbe5-172">例如，需要回收服務時會顯示黃色回收符號。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-172">For example, a yellow recycle symbol is displayed if a service needs to be recycled.</span></span>

![服務提要欄位](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="dcbe5-174">不同 HDInsight 叢集類型和版本之間會顯示不同的服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-174">The services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="dcbe5-175">這裡顯示的服務可能會不同於您的叢集所顯示的服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-175">The services displayed here may be different than the services displayed for your cluster.</span></span>

<span data-ttu-id="dcbe5-176">選取服務便會顯示服務的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-176">Selecting a service displays more detailed information on the service.</span></span>

![服務摘要資訊](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="dcbe5-178">快速連結</span><span class="sxs-lookup"><span data-stu-id="dcbe5-178">Quick links</span></span>

<span data-ttu-id="dcbe5-179">某些服務會在頁面頂端顯示 [ **快速連結** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-179">Some services display a **Quick Links** link at the top of the page.</span></span> <span data-ttu-id="dcbe5-180">此連結可用來存取服務特定的 Web UI，例如：</span><span class="sxs-lookup"><span data-stu-id="dcbe5-180">This can be used to access service-specific web UIs, such as:</span></span>

* <span data-ttu-id="dcbe5-181">**作業記錄** - MapReduce 作業記錄。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="dcbe5-182">**資源管理員** - YARN ResourceManager UI。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="dcbe5-183">**NameNode** - Hadoop 分散式檔案系統 (HDFS) NameNode UI。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="dcbe5-184">**Oozie Web UI** - Oozie UI。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="dcbe5-185">選取任何一個連結便會在瀏覽器中開啟新索引標籤以顯示選取的頁面。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-185">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="dcbe5-186">對服務選取 [快速連結] 項目可能會傳回「找不到伺服器」的錯誤。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-186">Selecting the **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="dcbe5-187">如果您遇到這個錯誤，在對此服務使用 [快速連結] 項目時，您必須使用 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-187">If you encounter this error, you must use an SSH tunnel when using the **Quick Links** entry for this service.</span></span> <span data-ttu-id="dcbe5-188">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="dcbe5-189">管理</span><span class="sxs-lookup"><span data-stu-id="dcbe5-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="dcbe5-190">Ambari 使用者、群組和權限</span><span class="sxs-lookup"><span data-stu-id="dcbe5-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="dcbe5-191">使用[已加入網域](hdinsight-domain-joined-introduction.md)的 HDInsight 叢集時，支援處理使用者、群組和權限。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="dcbe5-192">如需在已加入網域之叢集上使用 Ambari 管理 UI 的相關資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-192">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="dcbe5-193">請勿變更以 Linux 為基礎之 HDInsight 叢集上的 Ambari 看門狗 (hdinsightwatchdog) 密碼。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-193">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="dcbe5-194">變更密碼會破壞在叢集上使用指令碼動作或執行調整作業的能力。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-194">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="dcbe5-195">主機</span><span class="sxs-lookup"><span data-stu-id="dcbe5-195">Hosts</span></span>

<span data-ttu-id="dcbe5-196">[ **主機** ] 頁面會列出叢集中的所有主機。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-196">The **Hosts** page lists all hosts in the cluster.</span></span> <span data-ttu-id="dcbe5-197">若要管理主機，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-197">To manage hosts, follow these steps.</span></span>

![主機頁面](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="dcbe5-199">使用 HDInsight 叢集時，請勿新增、解除委任或重新委任主機。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="dcbe5-200">選取您想要管理的主機。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-200">Select the host that you wish to manage.</span></span>

2. <span data-ttu-id="dcbe5-201">使用 [ **動作** ] 功能表，選擇您想要執行的動作：</span><span class="sxs-lookup"><span data-stu-id="dcbe5-201">Use the **Actions** menu to select the action that you wish to perform:</span></span>

   * <span data-ttu-id="dcbe5-202">**啟動所有元件** - 啟動主機上的所有元件。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-202">**Start all components** - Start all components on the host.</span></span>

   * <span data-ttu-id="dcbe5-203">**停止所有元件** - 停止主機上的所有元件。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-203">**Stop all components** - Stop all components on the host.</span></span>

   * <span data-ttu-id="dcbe5-204">**重新啟動所有元件** - 先停止再啟動主機上的所有元件。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-204">**Restart all components** - Stop and start all components on the host.</span></span>

   * <span data-ttu-id="dcbe5-205">**開啟維護模式** - 隱藏主機的警示。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-205">**Turn on maintenance mode** - Suppresses alerts for the host.</span></span> <span data-ttu-id="dcbe5-206">如果您執行的動作會產生警示，則應該啟用此模式。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="dcbe5-207">例如，停止和啟動服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="dcbe5-208">**關閉維護模式** - 讓主機恢復正常警示功能。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-208">**Turn off maintenance mode** - Returns the host to normal alerting.</span></span>

   * <span data-ttu-id="dcbe5-209">**停止** - 停止主機上的 DataNode 或 NodeManagers。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-209">**Stop** - Stops DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="dcbe5-210">**啟動** - 啟動主機上的 DataNode 或 NodeManagers。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-210">**Start** - Starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="dcbe5-211">**重新啟動** - 先停止再啟動主機上的 DataNode 或 NodeManagers。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-211">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="dcbe5-212">**解除委任** - 從叢集中移除主機。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-212">**Decommission** - Removes a host from the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="dcbe5-213">請勿在 HDInsight 叢集上使用此動作。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="dcbe5-214">**重新委任** - 將先前已解除委任的主機加入到叢集中。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-214">**Recommission** - Adds a previously decommissioned host to the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="dcbe5-215">請勿在 HDInsight 叢集上使用此動作。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="dcbe5-216"><a id="service"></a>服務</span><span class="sxs-lookup"><span data-stu-id="dcbe5-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="dcbe5-217">在 [儀表板] 或 [服務] 頁面中，使用服務清單底部的 [動作] 按鈕來停止和啟動所有服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-217">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span></span>

![服務動作](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="dcbe5-219">雖然 [新增服務] 列在此功能表中，但不應用來將服務新增 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-219">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span></span> <span data-ttu-id="dcbe5-220">您應該在叢集佈建期間，使用指令碼動作加入新服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="dcbe5-221">如需使用指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="dcbe5-222">雖然 [ **動作** ] 按鈕可以重新啟動所有服務，但您想要啟動、停止或重新啟動的往往是特定服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-222">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span></span> <span data-ttu-id="dcbe5-223">使用下列步驟可對個別服務執行動作：</span><span class="sxs-lookup"><span data-stu-id="dcbe5-223">Use the following steps to perform actions on an individual service:</span></span>

1. <span data-ttu-id="dcbe5-224">從 [儀表板] 或 [服務] 頁面選取服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-224">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="dcbe5-225">從 [摘要] 索引標籤頂端，使用 [服務動作] 按鈕，然後選取要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-225">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span></span> <span data-ttu-id="dcbe5-226">這會重新啟動所有節點上的服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-226">This restarts the service on all nodes.</span></span>

    ![服務動作](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="dcbe5-228">在叢集執行時重新啟動某些服務可能會產生警示。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-228">Restarting some services while the cluster is running may generate alerts.</span></span> <span data-ttu-id="dcbe5-229">若要避免警示，您可以使用 [服務動作] 按鈕來啟用服務的 [維護模式]，然後再執行重新啟動。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-229">To avoid alerts, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span></span>

3. <span data-ttu-id="dcbe5-230">一旦選取某個動作，頁面頂端的 [# 項作業] 項目便會遞增數字，指出正在進行背景作業。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-230">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span></span> <span data-ttu-id="dcbe5-231">如果設定為顯示，則會顯示背景作業的清單。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-231">If configured to display, the list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dcbe5-232">如果您已啟用服務的 [維護模式]，請記得在作業完成後使用 [服務動作] 按鈕來將它停用。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-232">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span></span>

<span data-ttu-id="dcbe5-233">若要設定服務，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dcbe5-233">To configure a service, use the following steps:</span></span>

1. <span data-ttu-id="dcbe5-234">從 [儀表板] 或 [服務] 頁面選取服務。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-234">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="dcbe5-235">選取 [ **設定** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-235">Select the **Configs** tab.</span></span> <span data-ttu-id="dcbe5-236">隨即會顯示目前的組態。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-236">The current configuration is displayed.</span></span> <span data-ttu-id="dcbe5-237">同時也會顯示先前組態的清單。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-237">A list of previous configurations is also displayed.</span></span>

    ![組態](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="dcbe5-239">使用顯示的欄位修改組態，然後選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-239">Use the fields displayed to modify the configuration, and then select **Save**.</span></span> <span data-ttu-id="dcbe5-240">或選取先前的組態，然後選取 [ **設為現用** ] 以回復到先前的設定。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-240">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="dcbe5-241">Ambari 檢視</span><span class="sxs-lookup"><span data-stu-id="dcbe5-241">Ambari views</span></span>

<span data-ttu-id="dcbe5-242">Ambari 檢視可讓開發人員使用 [Ambari 檢視架構](https://cwiki.apache.org/confluence/display/AMBARI/Views)將 UI 元素插入 Ambari Web UI 中。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-242">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="dcbe5-243">HDInsight 提供下列具有 Hadoop 叢集類型的檢視：</span><span class="sxs-lookup"><span data-stu-id="dcbe5-243">HDInsight provides the following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="dcbe5-244">Yarn 佇列管理員：佇列管理員提供簡單的 UI 以用於檢視及修改 YARN 佇列。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-244">Yarn Queue Manager: The queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="dcbe5-245">Hive 檢視：Hive 檢視可讓您直接從網頁瀏覽器執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-245">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span></span> <span data-ttu-id="dcbe5-246">您可以儲存查詢、檢視結果、將結果儲存至叢集存放區，或將結果下載到您本機系統。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-246">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span></span> <span data-ttu-id="dcbe5-247">如需有關使用 Hive 檢視的詳細資訊，請參閱 [在 HDInsight 上使用 Hive 檢視](hdinsight-hadoop-use-hive-ambari-view.md)。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-247">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="dcbe5-248">Tez 檢視︰[Tez 檢視] 可讓您進一步了解和最佳化工作。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-248">Tez View: The Tez View allows you to better understand and optimize jobs.</span></span> <span data-ttu-id="dcbe5-249">您可以檢視有關 Tez 工作執行方式及使用哪些資源的資訊。</span><span class="sxs-lookup"><span data-stu-id="dcbe5-249">You can view information on how Tez jobs are executed and what resources are used.</span></span>
