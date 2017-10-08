---
title: "aaaMonitor 和管理 Azure HDInsight 使用 Ambari Web UI |Microsoft 文件"
description: "深入了解如何 toouse Ambari toomonitor 和管理以 Linux 為基礎的 HDInsight 叢集。 在本文件中，您學會如何 toouse hello Ambari Web UI，包含與 HDInsight 叢集。"
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
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="06bc8-104">使用 hello Ambari Web UI 來管理 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="06bc8-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="06bc8-105">Apache Ambari 簡化 hello 的管理和監視 Hadoop 叢集藉由提供簡單 toouse web UI 和 REST API。</span><span class="sxs-lookup"><span data-stu-id="06bc8-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="06bc8-106">Ambari 包含以 Linux 為基礎的 HDInsight 叢集上，而且是使用的 toomonitor hello 叢集並設定變更。</span><span class="sxs-lookup"><span data-stu-id="06bc8-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="06bc8-107">在本文件中，您學會如何 toouse hello 與 HDInsight 叢集的 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="06bc8-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="06bc8-108"><a id="whatis"></a>什麼是 Ambari？</span><span class="sxs-lookup"><span data-stu-id="06bc8-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="06bc8-109">[Apache Ambari](http://ambari.apache.org) 提供方便使用的 Web UI，簡化 Hadoop 管理。</span><span class="sxs-lookup"><span data-stu-id="06bc8-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="06bc8-110">您可以使用 Ambari 建立、管理及監視 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="06bc8-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="06bc8-111">開發人員可以這些功能整合到應用程式使用 hello [Ambari REST Api](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。</span><span class="sxs-lookup"><span data-stu-id="06bc8-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="06bc8-112">與使用 hello Linux 作業系統的 HDInsight 叢集預設會提供 hello Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="06bc8-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06bc8-113">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="06bc8-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="06bc8-114">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="06bc8-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="06bc8-115">連線能力</span><span class="sxs-lookup"><span data-stu-id="06bc8-115">Connectivity</span></span>

<span data-ttu-id="06bc8-116">hello Ambari Web UI 並用於您的 HDInsight 叢集 HTTPS://CLUSTERNAME.azurehdidnsight.net，在其中**CLUSTERNAME**是 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="06bc8-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06bc8-117">連接 tooAmbari HDInsight 上的需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="06bc8-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="06bc8-118">出現提示時進行驗證，使用 hello 管理帳戶名稱和密碼建立 hello 叢集時，您提供。</span><span class="sxs-lookup"><span data-stu-id="06bc8-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="06bc8-119">SSH 通道 (Proxy)</span><span class="sxs-lookup"><span data-stu-id="06bc8-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="06bc8-120">Ambari 叢集可以存取直接透過網際網路 hello，而某些連結從 hello Ambari Web UI （例如 toohello JobTracker) 不會公開在 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="06bc8-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="06bc8-121">tooaccess 這些服務，您必須建立 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="06bc8-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="06bc8-122">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)。</span><span class="sxs-lookup"><span data-stu-id="06bc8-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="06bc8-123">Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="06bc8-123">Ambari Web UI</span></span>

<span data-ttu-id="06bc8-124">當連線 toohello Ambari Web UI，您會使用提示的 tooauthenticate toohello page。</span><span class="sxs-lookup"><span data-stu-id="06bc8-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="06bc8-125">使用 hello 叢集系統管理員使用者 （預設系統管理員） 和您在叢集建立期間使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="06bc8-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="06bc8-126">當 hello 頁面隨即開啟時，請注意在 hello 最上方的 hello 列。</span><span class="sxs-lookup"><span data-stu-id="06bc8-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="06bc8-127">這個列中的 hello 下列資訊和控制項：</span><span class="sxs-lookup"><span data-stu-id="06bc8-127">This bar contains hello following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="06bc8-129">**Ambari 標誌**-開啟 hello 儀表板，它可以是使用的 toomonitor hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="06bc8-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="06bc8-130">**叢集名稱 # ops** -顯示 hello Ambari 作業數目。</span><span class="sxs-lookup"><span data-stu-id="06bc8-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="06bc8-131">選取的 hello 叢集名稱或**# ops**顯示背景作業的清單。</span><span class="sxs-lookup"><span data-stu-id="06bc8-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="06bc8-132">**# 警示**-顯示警告或重大警示，如果有 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="06bc8-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="06bc8-133">**儀表板**-顯示 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="06bc8-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="06bc8-134">**服務**-hello 叢集中的 hello 服務的資訊和組態設定。</span><span class="sxs-lookup"><span data-stu-id="06bc8-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="06bc8-135">**主機**-hello hello 叢集中節點的資訊和組態設定。</span><span class="sxs-lookup"><span data-stu-id="06bc8-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="06bc8-136">**警示** - 資訊、警告和重要警示的記錄。</span><span class="sxs-lookup"><span data-stu-id="06bc8-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="06bc8-137">**系統管理員**-軟體堆疊/服務安裝在 hello 叢集、 服務帳戶資訊，以及 Kerberos 安全性。</span><span class="sxs-lookup"><span data-stu-id="06bc8-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="06bc8-138">**系統管理員按鈕** - Ambari 管理、使用者設定和登出。</span><span class="sxs-lookup"><span data-stu-id="06bc8-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="06bc8-139">監視</span><span class="sxs-lookup"><span data-stu-id="06bc8-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="06bc8-140">Alerts</span><span class="sxs-lookup"><span data-stu-id="06bc8-140">Alerts</span></span>

<span data-ttu-id="06bc8-141">hello 下列清單包含常見 hello 使用 Ambari 警示狀態：</span><span class="sxs-lookup"><span data-stu-id="06bc8-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="06bc8-142">**確定**</span><span class="sxs-lookup"><span data-stu-id="06bc8-142">**OK**</span></span>
* <span data-ttu-id="06bc8-143">**警告**</span><span class="sxs-lookup"><span data-stu-id="06bc8-143">**Warning**</span></span>
* <span data-ttu-id="06bc8-144">**重要**</span><span class="sxs-lookup"><span data-stu-id="06bc8-144">**CRITICAL**</span></span>
* <span data-ttu-id="06bc8-145">**未知**</span><span class="sxs-lookup"><span data-stu-id="06bc8-145">**UNKNOWN**</span></span>

<span data-ttu-id="06bc8-146">警示以外**確定**導致 hello **# 警示**頂端 hello hello 頁面 toodisplay hello 警示數目的項目。</span><span class="sxs-lookup"><span data-stu-id="06bc8-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="06bc8-147">選取此項目會顯示 hello 警示和狀態。</span><span class="sxs-lookup"><span data-stu-id="06bc8-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="06bc8-148">警示會分成數個預設群組，可檢視從 hello**警示**頁面。</span><span class="sxs-lookup"><span data-stu-id="06bc8-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![警示頁面](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="06bc8-150">您可以使用 hello 管理 hello 群組**動作**功能表，然後選取**管理警示的群組**。</span><span class="sxs-lookup"><span data-stu-id="06bc8-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![管理警示群組對話方塊](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="06bc8-152">您也可以管理警示的方法，並從 hello 建立警示通知**動作**功能表選取__管理警示通知__。</span><span class="sxs-lookup"><span data-stu-id="06bc8-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="06bc8-153">系統會顯示任何目前的通知。</span><span class="sxs-lookup"><span data-stu-id="06bc8-153">Any current notifications are displayed.</span></span> <span data-ttu-id="06bc8-154">您也可以從這裡建立通知。</span><span class="sxs-lookup"><span data-stu-id="06bc8-154">You can also create notifications from here.</span></span> <span data-ttu-id="06bc8-155">在發生特定警示/嚴重性組合時，便可透過**電子郵件**或 **SNMP** 傳送通知。</span><span class="sxs-lookup"><span data-stu-id="06bc8-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="06bc8-156">例如，您可以傳送 hello 的電子郵件訊息時 hello 警示的任何**YARN 預設**群組設定得**重大**。</span><span class="sxs-lookup"><span data-stu-id="06bc8-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![建立警示對話方塊](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="06bc8-158">最後，選取__管理警示設定__從 hello__動作__功能表可讓您 tooset hello 警示必須出現次數之前，會傳送通知。</span><span class="sxs-lookup"><span data-stu-id="06bc8-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="06bc8-159">此設定可使用的 tooprevent 暫時性錯誤的通知。</span><span class="sxs-lookup"><span data-stu-id="06bc8-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="06bc8-160">叢集</span><span class="sxs-lookup"><span data-stu-id="06bc8-160">Cluster</span></span>

<span data-ttu-id="06bc8-161">hello**度量**hello 儀表板 索引標籤包含一系列，可讓您輕鬆 toomonitor hello 狀態，在叢集的一眼 widget。</span><span class="sxs-lookup"><span data-stu-id="06bc8-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="06bc8-162">[ **CPU 使用量**] 等數個 Widget 可在點按後提供其他資訊。</span><span class="sxs-lookup"><span data-stu-id="06bc8-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![儀表板與度量](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="06bc8-164">hello **Heatmaps**  索引標籤會顯示為彩色 heatmaps，從綠色 toored 的度量。</span><span class="sxs-lookup"><span data-stu-id="06bc8-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![儀表板與熱圖](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="06bc8-166">如需有關 hello 叢集內的 hello 節點的詳細資訊，請選取**主機**。</span><span class="sxs-lookup"><span data-stu-id="06bc8-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="06bc8-167">然後，選取您感興趣的 hello 特定節點。</span><span class="sxs-lookup"><span data-stu-id="06bc8-167">Then select hello specific node you are interested in.</span></span>

![主機詳細資料](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="06bc8-169">服務</span><span class="sxs-lookup"><span data-stu-id="06bc8-169">Services</span></span>

<span data-ttu-id="06bc8-170">hello**服務**hello 儀表板上的資訊看板提供快速了解 hello hello hello 叢集上執行的服務狀態。</span><span class="sxs-lookup"><span data-stu-id="06bc8-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="06bc8-171">不同的圖示是使用的 tooindicate 狀態或應該採取的動作。</span><span class="sxs-lookup"><span data-stu-id="06bc8-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="06bc8-172">例如，如果服務需要 toobe 回收，會顯示黃色回收符號。</span><span class="sxs-lookup"><span data-stu-id="06bc8-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![服務提要欄位](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="06bc8-174">顯示 hello 服務不同 HDInsight 叢集的型別和版本。</span><span class="sxs-lookup"><span data-stu-id="06bc8-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="06bc8-175">此處顯示的 hello 服務可能不同於 hello 服務顯示為您的叢集。</span><span class="sxs-lookup"><span data-stu-id="06bc8-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="06bc8-176">選取服務會更詳細的資訊顯示 hello 服務上。</span><span class="sxs-lookup"><span data-stu-id="06bc8-176">Selecting a service displays more detailed information on hello service.</span></span>

![服務摘要資訊](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="06bc8-178">快速連結</span><span class="sxs-lookup"><span data-stu-id="06bc8-178">Quick links</span></span>

<span data-ttu-id="06bc8-179">某些服務顯示**快速連結**hello hello 頁頂端的連結。</span><span class="sxs-lookup"><span data-stu-id="06bc8-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="06bc8-180">這可以是使用的 tooaccess 特定服務的 web Ui，例如：</span><span class="sxs-lookup"><span data-stu-id="06bc8-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="06bc8-181">**作業記錄** - MapReduce 作業記錄。</span><span class="sxs-lookup"><span data-stu-id="06bc8-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="06bc8-182">**資源管理員** - YARN ResourceManager UI。</span><span class="sxs-lookup"><span data-stu-id="06bc8-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="06bc8-183">**NameNode** - Hadoop 分散式檔案系統 (HDFS) NameNode UI。</span><span class="sxs-lookup"><span data-stu-id="06bc8-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="06bc8-184">**Oozie Web UI** - Oozie UI。</span><span class="sxs-lookup"><span data-stu-id="06bc8-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="06bc8-185">選取任何這些連結，則會在瀏覽器中顯示 hello 選取的頁面開啟新索引標籤。</span><span class="sxs-lookup"><span data-stu-id="06bc8-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="06bc8-186">選取 hello**快速連結**服務項目可能會傳回 「 找不到伺服器 」 錯誤。</span><span class="sxs-lookup"><span data-stu-id="06bc8-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="06bc8-187">如果您遇到這個錯誤，您就必須使用 SSH 通道，當使用 hello**快速連結**這個服務項目。</span><span class="sxs-lookup"><span data-stu-id="06bc8-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="06bc8-188">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)。</span><span class="sxs-lookup"><span data-stu-id="06bc8-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="06bc8-189">管理</span><span class="sxs-lookup"><span data-stu-id="06bc8-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="06bc8-190">Ambari 使用者、群組和權限</span><span class="sxs-lookup"><span data-stu-id="06bc8-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="06bc8-191">使用[已加入網域](hdinsight-domain-joined-introduction.md)的 HDInsight 叢集時，支援處理使用者、群組和權限。</span><span class="sxs-lookup"><span data-stu-id="06bc8-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="06bc8-192">如需使用 hello Ambari 管理 UI 已加入網域的叢集上的資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="06bc8-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="06bc8-193">請勿變更 hello 以 Linux 為基礎的 HDInsight 叢集上的 hello Ambari 監視 (hdinsightwatchdog) 密碼。</span><span class="sxs-lookup"><span data-stu-id="06bc8-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="06bc8-194">變更 hello 密碼符號 hello 能力 toouse 指令碼動作，或執行與您的叢集的調整作業。</span><span class="sxs-lookup"><span data-stu-id="06bc8-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="06bc8-195">主機</span><span class="sxs-lookup"><span data-stu-id="06bc8-195">Hosts</span></span>

<span data-ttu-id="06bc8-196">hello**主機**頁面會列出 hello 叢集中所有主機。</span><span class="sxs-lookup"><span data-stu-id="06bc8-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="06bc8-197">toomanage 主機，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="06bc8-197">toomanage hosts, follow these steps.</span></span>

![主機頁面](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="06bc8-199">使用 HDInsight 叢集時，請勿新增、解除委任或重新委任主機。</span><span class="sxs-lookup"><span data-stu-id="06bc8-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="06bc8-200">選取您想 toomanage hello 主機。</span><span class="sxs-lookup"><span data-stu-id="06bc8-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="06bc8-201">使用 hello**動作**想 tooperform 功能表 tooselect hello 動作：</span><span class="sxs-lookup"><span data-stu-id="06bc8-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="06bc8-202">**啟動所有元件**-hello 主機上都啟動所有元件。</span><span class="sxs-lookup"><span data-stu-id="06bc8-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="06bc8-203">**停止所有元件**-hello 主機上都停止所有元件。</span><span class="sxs-lookup"><span data-stu-id="06bc8-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="06bc8-204">**重新啟動所有元件**-停止並啟動 hello 主機上的所有元件。</span><span class="sxs-lookup"><span data-stu-id="06bc8-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="06bc8-205">**啟動維護模式**-會歸併警示 hello 主機。</span><span class="sxs-lookup"><span data-stu-id="06bc8-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="06bc8-206">如果您執行的動作會產生警示，則應該啟用此模式。</span><span class="sxs-lookup"><span data-stu-id="06bc8-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="06bc8-207">例如，停止和啟動服務。</span><span class="sxs-lookup"><span data-stu-id="06bc8-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="06bc8-208">**將維護模式關閉**-傳回 hello 主機 toonormal 警示。</span><span class="sxs-lookup"><span data-stu-id="06bc8-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="06bc8-209">**停止**-停駐點 DataNode 或 NodeManagers hello 主機上的。</span><span class="sxs-lookup"><span data-stu-id="06bc8-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="06bc8-210">**啟動**-啟動 DataNode 或 NodeManagers hello 主機上的。</span><span class="sxs-lookup"><span data-stu-id="06bc8-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="06bc8-211">**重新啟動**-停止或啟動 DataNode 或 NodeManagers hello 主機上的。</span><span class="sxs-lookup"><span data-stu-id="06bc8-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="06bc8-212">**解除委任**-從 hello 叢集移除主機。</span><span class="sxs-lookup"><span data-stu-id="06bc8-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="06bc8-213">請勿在 HDInsight 叢集上使用此動作。</span><span class="sxs-lookup"><span data-stu-id="06bc8-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="06bc8-214">**Recommission** -新增先前已解除委任的主機 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="06bc8-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="06bc8-215">請勿在 HDInsight 叢集上使用此動作。</span><span class="sxs-lookup"><span data-stu-id="06bc8-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="06bc8-216"><a id="service"></a>服務</span><span class="sxs-lookup"><span data-stu-id="06bc8-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="06bc8-217">從 hello**儀表板**或**服務**頁面上，使用 hello**動作**在 hello 服務 toostop hello 清單底部的按鈕，並啟動所有服務。</span><span class="sxs-lookup"><span data-stu-id="06bc8-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![服務動作](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="06bc8-219">雖然**加入服務**會列在這個功能表中，不應該使用的 tooadd 服務 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="06bc8-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="06bc8-220">您應該在叢集佈建期間，使用指令碼動作加入新服務。</span><span class="sxs-lookup"><span data-stu-id="06bc8-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="06bc8-221">如需使用指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="06bc8-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="06bc8-222">Hello 時**動作**按鈕可以重新啟動所有服務，通常您會想 toostart、 停止或重新都啟動特定的服務。</span><span class="sxs-lookup"><span data-stu-id="06bc8-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="06bc8-223">使用下列步驟 tooperform 動作上的個別服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="06bc8-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="06bc8-224">從 hello**儀表板**或**服務**頁面上，選取服務。</span><span class="sxs-lookup"><span data-stu-id="06bc8-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="06bc8-225">從 hello 頂端 hello**摘要**索引標籤上，使用 hello**服務動作**按鈕並選取 hello 動作 tootake。</span><span class="sxs-lookup"><span data-stu-id="06bc8-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="06bc8-226">這會重新啟動所有節點上的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="06bc8-226">This restarts hello service on all nodes.</span></span>

    ![服務動作](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="06bc8-228">Hello 叢集正在執行，請重新啟動某些服務可能會產生警示。</span><span class="sxs-lookup"><span data-stu-id="06bc8-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="06bc8-229">tooavoid 發出警示通知，您可以使用 hello**服務動作**按鈕 tooenable**維護模式**hello 服務，然後再執行 hello 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="06bc8-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="06bc8-230">一旦選取動作，hello **# op**在背景作業發生的 hello 頁面遞增 tooshow hello 最上方的項目。</span><span class="sxs-lookup"><span data-stu-id="06bc8-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="06bc8-231">如果設定 toodisplay，會顯示 hello 背景作業清單。</span><span class="sxs-lookup"><span data-stu-id="06bc8-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="06bc8-232">如果您啟用**維護模式**hello 服務，請記住 toodisable 它使用 hello**服務動作**按鈕一旦 hello 作業已完成。</span><span class="sxs-lookup"><span data-stu-id="06bc8-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="06bc8-233">tooconfigure 服務時，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="06bc8-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="06bc8-234">從 hello**儀表板**或**服務**頁面上，選取服務。</span><span class="sxs-lookup"><span data-stu-id="06bc8-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="06bc8-235">選取 hello **Configs**  索引標籤 hello 的目前組態會顯示。</span><span class="sxs-lookup"><span data-stu-id="06bc8-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="06bc8-236">同時也會顯示先前組態的清單。</span><span class="sxs-lookup"><span data-stu-id="06bc8-236">A list of previous configurations is also displayed.</span></span>

    ![組態](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="06bc8-238">使用 hello 顯示欄位 toomodify hello 組態，然後選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="06bc8-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="06bc8-239">或選取先前的設定，然後選取**設為現用**tooroll 回 toohello 先前的設定。</span><span class="sxs-lookup"><span data-stu-id="06bc8-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="06bc8-240">Ambari 檢視</span><span class="sxs-lookup"><span data-stu-id="06bc8-240">Ambari views</span></span>

<span data-ttu-id="06bc8-241">Ambari 檢視可讓開發人員 tooplug UI 項目到 hello Ambari Web UI 使用 hello [Ambari 檢視 Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views)。</span><span class="sxs-lookup"><span data-stu-id="06bc8-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="06bc8-242">HDInsight 提供下列檢視與 Hadoop 叢集類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="06bc8-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="06bc8-243">Yarn 佇列管理員： hello 佇列管理員提供的簡單 UI 的檢視和修改 YARN 佇列。</span><span class="sxs-lookup"><span data-stu-id="06bc8-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="06bc8-244">登錄區檢視： hello hive 控制檔的檢視可讓您直接從您網頁瀏覽器 toorun Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="06bc8-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="06bc8-245">您可以儲存查詢、 檢視結果、 將結果儲存 toohello 叢集存放裝置，或下載結果 tooyour 本機系統。</span><span class="sxs-lookup"><span data-stu-id="06bc8-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="06bc8-246">如需有關使用 Hive 檢視的詳細資訊，請參閱 [在 HDInsight 上使用 Hive 檢視](hdinsight-hadoop-use-hive-ambari-view.md)。</span><span class="sxs-lookup"><span data-stu-id="06bc8-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="06bc8-247">Tez 檢視： hello Tez 檢視可讓您 toobetter 了解並最佳化作業。</span><span class="sxs-lookup"><span data-stu-id="06bc8-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="06bc8-248">您可以檢視有關 Tez 工作執行方式及使用哪些資源的資訊。</span><span class="sxs-lookup"><span data-stu-id="06bc8-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
