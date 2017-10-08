---
title: "HDInsight linux 叢集-Azure 上的 Hadoop aaaHue |Microsoft 文件"
description: "了解 tooinstall 色調 HDInsight 上的叢集，並使用通道 tooroute hello 要求 tooHue。 使用 色調 toobrowse 儲存體，並執行 Hive 或 Pig。"
keywords: Hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="8f526-105">在 HDInsight Hadoop 叢集上安裝和使用 Hue</span><span class="sxs-lookup"><span data-stu-id="8f526-105">Install and use Hue on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="8f526-106">了解 tooinstall 色調 HDInsight 上的叢集，並使用通道 tooroute hello 要求 tooHue。</span><span class="sxs-lookup"><span data-stu-id="8f526-106">Learn how tooinstall Hue on HDInsight clusters and use tunneling tooroute hello requests tooHue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f526-107">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="8f526-107">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="8f526-108">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="8f526-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8f526-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="8f526-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-is-hue"></a><span data-ttu-id="8f526-110">何謂 Hue？</span><span class="sxs-lookup"><span data-stu-id="8f526-110">What is Hue?</span></span>
<span data-ttu-id="8f526-111">色調是一組 Web 應用程式使用 toointeract 與 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="8f526-111">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span> <span data-ttu-id="8f526-112">您可以使用相關聯的 Hadoop 叢集 (在 HDInsight 叢集的案例中 hello WASB) 的色調 toobrowse hello 儲存體、 執行工作 Hive 和 Pig 指令碼，並以此類推。</span><span class="sxs-lookup"><span data-stu-id="8f526-112">You can use Hue toobrowse hello storage associated with a Hadoop cluster (WASB, in hello case of HDInsight clusters), run Hive jobs and Pig scripts, and so on.</span></span> <span data-ttu-id="8f526-113">hello 下列元件都可以使用 HDInsight Hadoop 叢集上的色調安裝。</span><span class="sxs-lookup"><span data-stu-id="8f526-113">hello following components are available with Hue installations on an HDInsight Hadoop cluster.</span></span>

* <span data-ttu-id="8f526-114">Beeswax Hive 編輯器</span><span class="sxs-lookup"><span data-stu-id="8f526-114">Beeswax Hive Editor</span></span>
* <span data-ttu-id="8f526-115">Pig</span><span class="sxs-lookup"><span data-stu-id="8f526-115">Pig</span></span>
* <span data-ttu-id="8f526-116">Metastore 管理員</span><span class="sxs-lookup"><span data-stu-id="8f526-116">Metastore manager</span></span>
* <span data-ttu-id="8f526-117">Oozie</span><span class="sxs-lookup"><span data-stu-id="8f526-117">Oozie</span></span>
* <span data-ttu-id="8f526-118">FileBrowser （其中交談 tooWASB 預設容器）</span><span class="sxs-lookup"><span data-stu-id="8f526-118">FileBrowser (which talks tooWASB default container)</span></span>
* <span data-ttu-id="8f526-119">工作瀏覽器</span><span class="sxs-lookup"><span data-stu-id="8f526-119">Job Browser</span></span>

> [!WARNING]
> <span data-ttu-id="8f526-120">完全支援隨附 hello HDInsight 叢集的元件，而且 Microsoft 支援服務將會說明 tooisolate 及解決問題的相關的 toothese 元件。</span><span class="sxs-lookup"><span data-stu-id="8f526-120">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="8f526-121">自訂元件會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="8f526-121">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="8f526-122">這可能會導致解決 hello 問題，或詢問您 tooengage hello 可用的頻道開啟原始碼技術找到深層的專業知識，針對該項技術。</span><span class="sxs-lookup"><span data-stu-id="8f526-122">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="8f526-123">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="8f526-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
>
>

## <a name="install-hue-using-script-actions"></a><span data-ttu-id="8f526-124">使用指令碼動作安裝 Hue</span><span class="sxs-lookup"><span data-stu-id="8f526-124">Install Hue using Script Actions</span></span>

<span data-ttu-id="8f526-125">hello 指令碼 tooinstall 色調以 Linux 為基礎的 HDInsight 叢集上將會位於 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh。當做預設儲存體，您可以在與 Azure 儲存體 Blob (WASB) 或 Azure Data Lake Store 的叢集上使用此指令碼 tooinstall 色調。</span><span class="sxs-lookup"><span data-stu-id="8f526-125">hello script tooinstall Hue on a Linux-based HDInsight cluster is available at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. You can use this script tooinstall Hue on clusters with either Azure Storage Blobs (WASB) or Azure Data Lake Store as default storage.</span></span>

<span data-ttu-id="8f526-126">本節提供有關如何 toouse hello 指令碼佈建 hello 叢集使用 hello Azure 入口網站時的指示。</span><span class="sxs-lookup"><span data-stu-id="8f526-126">This section provides instructions about how toouse hello script when provisioning hello cluster using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="8f526-127">Azure PowerShell、 hello Azure CLI、 hello HDInsight.NET SDK 或 Azure 資源管理員範本也可以使用的 tooapply 指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="8f526-127">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="8f526-128">您也可以套用指令碼動作 tooalready 執行中的叢集。</span><span class="sxs-lookup"><span data-stu-id="8f526-128">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="8f526-129">如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="8f526-129">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="8f526-130">開始使用中的 hello 步驟佈建叢集[佈建 HDInsight 叢集在 Linux 上](hdinsight-hadoop-provision-linux-clusters.md)，但是不完成佈建。</span><span class="sxs-lookup"><span data-stu-id="8f526-130">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f526-131">tooinstall 色調 HDInsight 上的叢集、 hello 建議叢集前端節點大小至少為 A4 （8 核心，14 GB 記憶體）。</span><span class="sxs-lookup"><span data-stu-id="8f526-131">tooinstall Hue on HDInsight clusters, hello recommended headnode size is at least A4 (8 cores, 14 GB memory).</span></span>
   >
   >
2. <span data-ttu-id="8f526-132">在 hello**選擇性組態**刀鋒視窗中，選取**指令碼動作**，並提供 hello 資訊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8f526-132">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello information as shown below:</span></span>

    <span data-ttu-id="8f526-133">![提供 Hue 的指令碼動作參數](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "提供 Hue 的指令碼動作參數")</span><span class="sxs-lookup"><span data-stu-id="8f526-133">![Provide script action parameters for Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Provide script action parameters for Hue")</span></span>

   * <span data-ttu-id="8f526-134">**名稱**： 輸入 hello 指令碼動作的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="8f526-134">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="8f526-135">**SCRIPT URI**：https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh</span><span class="sxs-lookup"><span data-stu-id="8f526-135">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh</span></span>
   * <span data-ttu-id="8f526-136">**HEAD**：勾選此選項</span><span class="sxs-lookup"><span data-stu-id="8f526-136">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="8f526-137">**背景工作角色**：將此選項保留空白。</span><span class="sxs-lookup"><span data-stu-id="8f526-137">**WORKER**: Leave this blank.</span></span>
   * <span data-ttu-id="8f526-138">**ZOOKEEPER**：將此選項保留空白。</span><span class="sxs-lookup"><span data-stu-id="8f526-138">**ZOOKEEPER**: Leave this blank.</span></span>
   * <span data-ttu-id="8f526-139">**參數**：將此選項保留空白。</span><span class="sxs-lookup"><span data-stu-id="8f526-139">**PARAMETERS**: Leave this blank.</span></span>
3. <span data-ttu-id="8f526-140">在 hello 底部 hello**指令碼動作**，使用 hello**選取**按鈕 toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="8f526-140">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="8f526-141">最後，使用 hello**選取**在 hello hello 底部的按鈕**選擇性組態**刀鋒視窗 toosave hello 選擇性的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="8f526-141">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>
4. <span data-ttu-id="8f526-142">繼續中所述，佈建 hello 叢集[佈建 HDInsight 叢集在 Linux 上](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="8f526-142">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="use-hue-with-hdinsight-clusters"></a><span data-ttu-id="8f526-143">搭配使用 Hue 與 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="8f526-143">Use Hue with HDInsight clusters</span></span>

<span data-ttu-id="8f526-144">SSH 通道是 hello 唯一方式 tooaccess 色調 hello 叢集上的，一旦它正在執行。</span><span class="sxs-lookup"><span data-stu-id="8f526-144">SSH Tunneling is hello only way tooaccess Hue on hello cluster once it is running.</span></span> <span data-ttu-id="8f526-145">透過 SSH 通道可讓 hello 流量 toogo 直接 toohello 叢集前端節點的 hello 叢集正在色調。</span><span class="sxs-lookup"><span data-stu-id="8f526-145">Tunneling via SSH allows hello traffic toogo directly toohello headnode of hello cluster where Hue is running.</span></span> <span data-ttu-id="8f526-146">Hello 叢集佈建完成後，使用下列步驟 toouse 色調 HDInsight Linux 叢集上的 hello。</span><span class="sxs-lookup"><span data-stu-id="8f526-146">After hello cluster has finished provisioning, use hello following steps toouse Hue on an HDInsight Linux cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8f526-147">我們建議使用 Firefox web 瀏覽器 toofollow hello 下列指示。</span><span class="sxs-lookup"><span data-stu-id="8f526-147">We recommend using Firefox web browser toofollow hello instructions below.</span></span>
>
>

1. <span data-ttu-id="8f526-148">使用中的 hello 資訊[使用 SSH 通道 tooaccess Ambari web UI、 ResourceManager、 JobHistory、 NameNode、 Oozie、 以及其他的 web UI](hdinsight-linux-ambari-ssh-tunnel.md) toocreate SSH 通道，從用戶端系統 toohello HDInsight 叢集，然後再設定您 Web 瀏覽器 toouse hello SSH 通道的 proxy。</span><span class="sxs-lookup"><span data-stu-id="8f526-148">Use hello information in [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md) toocreate an SSH tunnel from your client system toohello HDInsight cluster, and then configure your Web browser toouse hello SSH tunnel as a proxy.</span></span>

2. <span data-ttu-id="8f526-149">一旦您建立的 SSH 通道並設定您的瀏覽器 tooproxy 流量透過它，您必須尋找 hello 的 hello 的主要前端節點的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="8f526-149">Once you have created an SSH tunnel and configured your browser tooproxy traffic through it, you must find hello host name of hello primary head node.</span></span> <span data-ttu-id="8f526-150">您可以連接 toohello 叢集使用 SSH 連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="8f526-150">You can do this by connecting toohello cluster using SSH on port 22.</span></span> <span data-ttu-id="8f526-151">比方說，`ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`其中**USERNAME**是您的 SSH 使用者名稱和**CLUSTERNAME**是 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="8f526-151">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` where **USERNAME** is your SSH user name and **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="8f526-152">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="8f526-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="8f526-153">一旦連接之後，使用下列命令 tooobtain hello 的 hello 主要叢集前端節點的完整的網域名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f526-153">Once connected, use hello following command tooobtain hello fully qualified domain name of hello primary headnode:</span></span>

        hostname -f

    <span data-ttu-id="8f526-154">這會傳回名稱類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="8f526-154">This will return a name similar toohello following:</span></span>

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    <span data-ttu-id="8f526-155">這是 hello 色調網站所在的 hello 主要叢集前端節點的 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="8f526-155">This is hello hostname of hello primary headnode where hello Hue website is located.</span></span>
4. <span data-ttu-id="8f526-156">使用 http://HOSTNAME:8888 hello 瀏覽器 tooopen hello 色調入口網站。</span><span class="sxs-lookup"><span data-stu-id="8f526-156">Use hello browser tooopen hello Hue portal at http://HOSTNAME:8888.</span></span> <span data-ttu-id="8f526-157">主機名稱取代 hello hello 先前步驟中取得的名稱。</span><span class="sxs-lookup"><span data-stu-id="8f526-157">Replace HOSTNAME with hello name you obtained in hello previous step.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f526-158">當您登入 hello 第一次時，您將會提示的 toocreate toohello 色調入口網站中的帳戶 toolog。</span><span class="sxs-lookup"><span data-stu-id="8f526-158">When you log in for hello first time, you will be prompted toocreate an account toolog in toohello Hue portal.</span></span> <span data-ttu-id="8f526-159">您在此處指定的 hello 認證將會限制的 toohello 入口網站，並不相關的 toohello 管理員或佈建 hello 叢集時所指定的 SSH 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="8f526-159">hello credentials you specify here will be limited toohello portal and are not related toohello admin or SSH user credentials you specified while provision hello cluster.</span></span>
   >
   >

    <span data-ttu-id="8f526-160">![登入 toohello 色調入口網站](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "指定認證色調入口網站")</span><span class="sxs-lookup"><span data-stu-id="8f526-160">![Login toohello Hue portal](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "Specify credentials for Hue portal")</span></span>

### <a name="run-a-hive-query"></a><span data-ttu-id="8f526-161">執行 HIVE 查詢</span><span class="sxs-lookup"><span data-stu-id="8f526-161">Run a Hive query</span></span>
1. <span data-ttu-id="8f526-162">從 hello 色調入口網站中，按一下 **查詢編輯器**，然後按一下 **Hive** tooopen hello 登錄區編輯器。</span><span class="sxs-lookup"><span data-stu-id="8f526-162">From hello Hue portal, click **Query Editors**, and then click **Hive** tooopen hello Hive editor.</span></span>

    <span data-ttu-id="8f526-163">![使用 Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "使用 Hive")</span><span class="sxs-lookup"><span data-stu-id="8f526-163">![Use Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Use Hive")</span></span>
2. <span data-ttu-id="8f526-164">在 hello**協助**索引標籤，下方**資料庫**，您應該會看到**hivesampletable**。</span><span class="sxs-lookup"><span data-stu-id="8f526-164">On hello **Assist** tab, under **Database**, you should see **hivesampletable**.</span></span> <span data-ttu-id="8f526-165">這是 HDInsight 上的所有 Hadoop 叢集隨附的範例資料表。</span><span class="sxs-lookup"><span data-stu-id="8f526-165">This is a sample table that is shipped with all Hadoop clusters on HDInsight.</span></span> <span data-ttu-id="8f526-166">輸入 hello 右窗格中的範例查詢和 hello 上看見 hello 輸出**結果**hello 螢幕擷取畫面所示，在下面 hello 窗格中索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8f526-166">Enter a sample query in hello right pane and see hello output on hello **Results** tab in hello pane below, as shown in hello screen capture.</span></span>

    <span data-ttu-id="8f526-167">![執行 Hive 查詢](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "執行 Hive 查詢")</span><span class="sxs-lookup"><span data-stu-id="8f526-167">![Run Hive query](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Run Hive query")</span></span>

    <span data-ttu-id="8f526-168">您也可以使用 hello**圖表**索引標籤上 toosee hello 結果的視覺化表示法。</span><span class="sxs-lookup"><span data-stu-id="8f526-168">You can also use hello **Chart** tab toosee a visual representation of hello result.</span></span>

### <a name="browse-hello-cluster-storage"></a><span data-ttu-id="8f526-169">瀏覽 hello 叢集存放裝置</span><span class="sxs-lookup"><span data-stu-id="8f526-169">Browse hello cluster storage</span></span>
1. <span data-ttu-id="8f526-170">從 hello 色調入口網站中，按一下 **檔案瀏覽器**hello 右上角中的 hello 功能表列中。</span><span class="sxs-lookup"><span data-stu-id="8f526-170">From hello Hue portal, click **File Browser** in hello top-right corner of hello menu bar.</span></span>
2. <span data-ttu-id="8f526-171">依預設 hello 檔案瀏覽器會開啟在 hello **/使用者/myuser**目錄。</span><span class="sxs-lookup"><span data-stu-id="8f526-171">By default hello file browser opens at hello **/user/myuser** directory.</span></span> <span data-ttu-id="8f526-172">按一下 前 hello hello toogo toohello 根路徑的 hello 與 hello 叢集相關聯的 Azure 儲存體容器中的使用者目錄的 hello 正斜線。</span><span class="sxs-lookup"><span data-stu-id="8f526-172">Click hello forward slash right before hello user directory in hello path toogo toohello root of hello Azure storage container associated with hello cluster.</span></span>

    <span data-ttu-id="8f526-173">![使用檔案瀏覽器](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "使用檔案瀏覽器")</span><span class="sxs-lookup"><span data-stu-id="8f526-173">![Use file browser](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "Use file browser")</span></span>
3. <span data-ttu-id="8f526-174">以滑鼠右鍵按一下檔案或資料夾 toosee hello 可用的作業。</span><span class="sxs-lookup"><span data-stu-id="8f526-174">Right-click on a file or folder toosee hello available operations.</span></span> <span data-ttu-id="8f526-175">使用 hello**上傳**hello 右上角 tooupload 檔案 toohello 目前目錄中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f526-175">Use hello **Upload** button in hello right corner tooupload files toohello current directory.</span></span> <span data-ttu-id="8f526-176">使用 hello**新增**按鈕 toocreate 新檔案或目錄。</span><span class="sxs-lookup"><span data-stu-id="8f526-176">Use hello **New** button toocreate new files or directories.</span></span>

> [!NOTE]
> <span data-ttu-id="8f526-177">hello 色調檔案瀏覽器只會顯示 hello 的 hello 與 hello HDInsight 叢集相關聯的預設容器的內容。</span><span class="sxs-lookup"><span data-stu-id="8f526-177">hello Hue file browser can only show hello contents of hello default container associated with hello HDInsight cluster.</span></span> <span data-ttu-id="8f526-178">任何額外的儲存體帳戶/容器，您可能有相關聯的 hello 叢集將無法存取使用 hello 檔案瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8f526-178">Any additional storage accounts/containers that you might have associated with hello cluster will not be accessible using hello file browser.</span></span> <span data-ttu-id="8f526-179">不過，hello 與 hello 叢集相關聯的其他容器永遠都可以存取 hello Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="8f526-179">However, hello additional containers associated with hello cluster will always be accessible for hello Hive jobs.</span></span> <span data-ttu-id="8f526-180">例如，如果您輸入 hello 命令`dfs -ls wasb://newcontainer@mystore.blob.core.windows.net`在 hello 登錄區編輯器 中，您可以看到 hello 內容以及其他容器。</span><span class="sxs-lookup"><span data-stu-id="8f526-180">For example, if you enter hello command `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` in hello Hive editor, you can see hello contents of additional containers as well.</span></span> <span data-ttu-id="8f526-181">這個命令中， **newcontainer**不 hello 與叢集相關聯的預設容器。</span><span class="sxs-lookup"><span data-stu-id="8f526-181">In this command, **newcontainer** is not hello default container associated with a cluster.</span></span>
>
>

## <a name="important-considerations"></a><span data-ttu-id="8f526-182">重要考量︰</span><span class="sxs-lookup"><span data-stu-id="8f526-182">Important considerations</span></span>
1. <span data-ttu-id="8f526-183">hello 用指令碼 tooinstall 色調會安裝它只能在 hello hello 叢集的主要前端節點上。</span><span class="sxs-lookup"><span data-stu-id="8f526-183">hello script used tooinstall Hue installs it only on hello primary headnode of hello cluster.</span></span>

2. <span data-ttu-id="8f526-184">在安裝期間，會重新啟動來更新 hello 組態的多個 Hadoop 服務 （HDFS、 YARN、 MR2、 Oozie）。</span><span class="sxs-lookup"><span data-stu-id="8f526-184">During installation, multiple Hadoop services (HDFS, YARN, MR2, Oozie) are restarted for updating hello configuration.</span></span> <span data-ttu-id="8f526-185">安裝色調的 hello 指令碼完成之後，它最多可能需要一些時間，其他的 Hadoop 服務 toostart。</span><span class="sxs-lookup"><span data-stu-id="8f526-185">After hello script finishes installing Hue, it might take some time for other Hadoop services toostart up.</span></span> <span data-ttu-id="8f526-186">一開始可能會影響 Hue 的效能。</span><span class="sxs-lookup"><span data-stu-id="8f526-186">This might affect Hue's performance initially.</span></span> <span data-ttu-id="8f526-187">所有服務啟動之後，Hue 就可以完全正常運作。</span><span class="sxs-lookup"><span data-stu-id="8f526-187">Once all services start up, Hue will be fully functional.</span></span>
3. <span data-ttu-id="8f526-188">色調不了解 Tez 作業 hello 登錄區的目前預設值。</span><span class="sxs-lookup"><span data-stu-id="8f526-188">Hue does not understand Tez jobs, which is hello current default for Hive.</span></span> <span data-ttu-id="8f526-189">如果您想 toouse MapReduce hello Hive 執行引擎時，，更新下列命令指令碼中的 hello 指令碼 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="8f526-189">If you want toouse MapReduce as hello Hive execution engine, update hello script toouse hello following command in your script:</span></span>

        set hive.execution.engine=mr;

4. <span data-ttu-id="8f526-190">使用 Linux 叢集時，您可以在您的服務正在執行的案例 hello 主要叢集前端節點上 hello 資源管理員無法執行 hello 次要上時。</span><span class="sxs-lookup"><span data-stu-id="8f526-190">With Linux clusters, you can have a scenario where your services are running on hello primary headnode while hello Resource Manager could be running on hello secondary.</span></span> <span data-ttu-id="8f526-191">Hello 叢集上使用的執行作業的色調 tooview 詳細資料時，這種狀況可能會導致錯誤 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="8f526-191">Such a scenario might result in errors (shown below) when using Hue tooview details of RUNNING jobs on hello cluster.</span></span> <span data-ttu-id="8f526-192">不過，您可以在 hello 作業完成時，檢視 hello 工作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8f526-192">However, you can view hello job details when hello job has completed.</span></span>

   <span data-ttu-id="8f526-193">![Hue 入口網站錯誤](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Hue 入口網站錯誤")</span><span class="sxs-lookup"><span data-stu-id="8f526-193">![Hue portal error](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Hue portal error")</span></span>

   <span data-ttu-id="8f526-194">這是因為 tooa 已知問題。</span><span class="sxs-lookup"><span data-stu-id="8f526-194">This is due tooa known issue.</span></span> <span data-ttu-id="8f526-195">因應措施，修改 Ambari 使 hello 作用中的資源管理員也會執行 hello 主要叢集前端節點上。</span><span class="sxs-lookup"><span data-stu-id="8f526-195">As a workaround, modify Ambari so that hello active Resource Manager also runs on hello primary headnode.</span></span>
5. <span data-ttu-id="8f526-196">當 HDInsight 叢集使用 Azure 儲存體 (使用 `wasb://`) 時，色調能了解 WebHDFS。</span><span class="sxs-lookup"><span data-stu-id="8f526-196">Hue understands WebHDFS while HDInsight clusters use Azure Storage using `wasb://`.</span></span> <span data-ttu-id="8f526-197">因此，hello 與指令碼動作搭配使用的自訂指令碼會安裝 WebWasb，是指 tooWASB WebHDFS 相容服務。</span><span class="sxs-lookup"><span data-stu-id="8f526-197">So, hello custom script used with script action installs WebWasb, which is a WebHDFS-compatible service for talking tooWASB.</span></span> <span data-ttu-id="8f526-198">因此，即使 hello 色調入口網站會指出 HDFS 位置中的 (例如當您將滑鼠移 hello**檔案瀏覽器**)，它應該解譯為 WASB。</span><span class="sxs-lookup"><span data-stu-id="8f526-198">So, even though hello Hue portal says HDFS in places (like when you move your mouse over hello **File Browser**), it should be interpreted as WASB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f526-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f526-199">Next steps</span></span>
* <span data-ttu-id="8f526-200">[在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="8f526-200">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="8f526-201">使用叢集自訂 tooinstall Giraph 上 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="8f526-201">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="8f526-202">Giraph 可讓您處理使用 Hadoop，tooperform 圖形，並搭配 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="8f526-202">Giraph allows you tooperform graph processing using Hadoop, and it can be used with Azure HDInsight.</span></span>
* <span data-ttu-id="8f526-203">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="8f526-203">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="8f526-204">使用叢集自訂 tooinstall Solr 上 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="8f526-204">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="8f526-205">Solr 可讓您儲存的資料 tooperform 功能強大的搜尋作業。</span><span class="sxs-lookup"><span data-stu-id="8f526-205">Solr allows you tooperform powerful search operations on stored data.</span></span>
* <span data-ttu-id="8f526-206">[在 HDInsight 叢集上安裝 R](hdinsight-hadoop-r-scripts-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="8f526-206">[Install R on HDInsight clusters](hdinsight-hadoop-r-scripts-linux.md).</span></span> <span data-ttu-id="8f526-207">使用叢集自訂 tooinstall R HDInsight Hadoop 叢集上。</span><span class="sxs-lookup"><span data-stu-id="8f526-207">Use cluster customization tooinstall R on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="8f526-208">R 是一個用於統計計算的開放原始碼語言和環境。</span><span class="sxs-lookup"><span data-stu-id="8f526-208">R is an open-source language and environment for statistical computing.</span></span> <span data-ttu-id="8f526-209">它提供數百個內建的統計函式及它自己的程式設計語言，此語言結合了函式型和物件導向程式設計的層面。</span><span class="sxs-lookup"><span data-stu-id="8f526-209">It provides hundreds of built-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="8f526-210">它也提供廣泛的圖形功能。</span><span class="sxs-lookup"><span data-stu-id="8f526-210">It also provides extensive graphical capabilities.</span></span>

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
