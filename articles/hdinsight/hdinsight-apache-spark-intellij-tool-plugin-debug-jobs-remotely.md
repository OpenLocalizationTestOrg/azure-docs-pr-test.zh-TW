---
title: "aaaAzure IntelliJ-在 HDInsight Spark 上遠端偵錯應用程式的工具組 |Microsoft 文件"
description: "深入了解如何在 Azure Toolkit 使用 HDInsight Tools for IntelliJ tooremotely 偵錯應用程式透過 vpn HDInsight Spark 叢集上執行。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="e98c5-103">使用 Azure Toolkit IntelliJ toodebug 上的應用程式從遠端透過 VPN HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="e98c5-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="e98c5-104">我們建議偵錯 spark applicaltion 從遠端透過 ssh 的 hello 的方法。</span><span class="sxs-lookup"><span data-stu-id="e98c5-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="e98c5-105">如需指示，請參閱[使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="e98c5-106">本文章提供如何 toouse hello IntelliJ toosubmit HDInsight Spark 叢集上的 Spark 作業在 Azure Toolkit HDInsight Tools，然後遠端偵錯它從您桌面的電腦上的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="e98c5-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="e98c5-107">toodo 因此，您必須執行下列高階步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="e98c5-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="e98c5-108">建立站對站或點對站 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e98c5-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="e98c5-109">本文件中的 hello 步驟假設您使用站對站網路。</span><span class="sxs-lookup"><span data-stu-id="e98c5-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="e98c5-110">建立屬於 hello-網站 Azure 虛擬網路的 Azure HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="e98c5-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="e98c5-111">確認 hello hello 叢集前端節點與您的桌面之間的連線。</span><span class="sxs-lookup"><span data-stu-id="e98c5-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="e98c5-112">在 IntelliJ IDEA 中建立 Scala 應用程式，並設定它以進行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="e98c5-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="e98c5-113">執行和偵錯 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e98c5-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e98c5-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="e98c5-114">Prerequisites</span></span>
* <span data-ttu-id="e98c5-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e98c5-115">An Azure subscription.</span></span> <span data-ttu-id="e98c5-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e98c5-117">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="e98c5-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e98c5-118">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="e98c5-119">Oracle Java Development Kit。</span><span class="sxs-lookup"><span data-stu-id="e98c5-119">Oracle Java Development kit.</span></span> <span data-ttu-id="e98c5-120">您可以從 [這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)加以安裝。</span><span class="sxs-lookup"><span data-stu-id="e98c5-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="e98c5-121">IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="e98c5-121">IntelliJ IDEA.</span></span> <span data-ttu-id="e98c5-122">本文章使用 2017.1 版。</span><span class="sxs-lookup"><span data-stu-id="e98c5-122">This article uses version 2017.1.</span></span> <span data-ttu-id="e98c5-123">您可以從[這裡](https://www.jetbrains.com/idea/download/)安裝它。</span><span class="sxs-lookup"><span data-stu-id="e98c5-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="e98c5-124">適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具。</span><span class="sxs-lookup"><span data-stu-id="e98c5-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="e98c5-125">HDInsight 工具 IntelliJ 可用 hello Azure Toolkit for IntelliJ 的一部分。</span><span class="sxs-lookup"><span data-stu-id="e98c5-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="e98c5-126">如需有關如何 tooinstall hello Azure Toolkit 的指示，請參閱[安裝 hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="e98c5-127">從 IntelliJ IDEA 登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e98c5-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="e98c5-128">請依照下列指示 hello[這裡](hdinsight-apache-spark-intellij-tool-plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="e98c5-129">在執行遠端偵錯在 Windows 電腦上的 Spark Scala 應用程式時，您可能會收到例外狀況中所述[SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) ，就會發生因為 tooa 遺漏 WinUtils.exe Windows 上的。</span><span class="sxs-lookup"><span data-stu-id="e98c5-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="e98c5-130">您必須解決此錯誤 toowork，[從這裡下載可執行檔的 hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 位置**C:\WinUtils\bin**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="e98c5-131">然後，您必須加入環境變數**HADOOP_HOME**並設定 hello hello 變數值太**C\WinUtils**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="e98c5-132">步驟 1：建立 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e98c5-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="e98c5-133">請依照下方連結 toocreate Azure 虛擬網路的 hello hello 指示，然後確認 hello hello 桌面和 Azure 虛擬網路之間的連線。</span><span class="sxs-lookup"><span data-stu-id="e98c5-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="e98c5-134">使用 Azure 入口網站建立具有站對站 VPN 連線的 VNet</span><span class="sxs-lookup"><span data-stu-id="e98c5-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="e98c5-135">使用 PowerShell 建立具有站對站 VPN 連線的 VNet</span><span class="sxs-lookup"><span data-stu-id="e98c5-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="e98c5-136">設定點對站連線 tooa 虛擬網路使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e98c5-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="e98c5-137">步驟 2：建立 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="e98c5-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="e98c5-138">您也應該屬於 hello 您建立 Azure 虛擬網路的 Azure HDInsight 上建立的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="e98c5-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="e98c5-139">使用可用的 hello 資訊[HDInsight 中的 建立 linux 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="e98c5-140">選擇性組態的一部分，選取 hello hello 先前步驟中所建立的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e98c5-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="e98c5-141">步驟 3： 確認 hello hello 叢集前端節點與您的桌面之間的連線</span><span class="sxs-lookup"><span data-stu-id="e98c5-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="e98c5-142">收到 hello 的 hello 叢集前端節點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e98c5-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="e98c5-143">開啟 hello 叢集 Ambari UI。</span><span class="sxs-lookup"><span data-stu-id="e98c5-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="e98c5-144">從 hello 叢集刀鋒視窗中，按一下 **儀表板**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="e98c5-146">從 hello Ambari UI 從 hello 右上角，按一下 **主機**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="e98c5-148">您應該會看到前端節點、背景工作角色節點和 zookeeper 節點的清單。</span><span class="sxs-lookup"><span data-stu-id="e98c5-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="e98c5-149">hello headnodes 擁有 hello **hn*** 前置詞。</span><span class="sxs-lookup"><span data-stu-id="e98c5-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="e98c5-150">按一下 hello 第一個前端節點。</span><span class="sxs-lookup"><span data-stu-id="e98c5-150">Click hello first headnode.</span></span>

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="e98c5-152">在 hello 開啟時，從 hello 的 hello 頁面底端**摘要**方塊中，複製 hello IP 位址的 hello 叢集前端節點和 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="e98c5-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="e98c5-154">包含 hello IP 位址和 hello 主機名稱的 hello 叢集前端節點 toohello**主機**hello 您想 toorun 和進行遠端偵錯 hello Spark 工作的電腦上的檔案。</span><span class="sxs-lookup"><span data-stu-id="e98c5-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="e98c5-155">這可讓您 toocommunicate 與 hello 叢集前端節點使用 hello IP 位址與 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="e98c5-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="e98c5-156">以提高的權限開啟 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="e98c5-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="e98c5-157">Hello 檔案 功能表中按一下**開啟**，然後瀏覽 toohello hello hosts 檔案位置。</span><span class="sxs-lookup"><span data-stu-id="e98c5-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="e98c5-158">在 Windows 電腦上，是 `C:\Windows\System32\Drivers\etc\hosts`。</span><span class="sxs-lookup"><span data-stu-id="e98c5-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="e98c5-159">新增下列 toohello hello**主機**檔案。</span><span class="sxs-lookup"><span data-stu-id="e98c5-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="e98c5-160">從 hello 連接 toohello hello HDInsight 叢集所使用的 Azure 虛擬網路的電腦，請確認您可以 ping hello IP 位址，以及 hello 主機名稱使用這兩個 hello headnodes。</span><span class="sxs-lookup"><span data-stu-id="e98c5-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="e98c5-161">SSH 到 hello 叢集前端節點使用 hello 指示[使用 SSH 連線 tooan HDInsight 叢集](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="e98c5-162">Hello 叢集前端節點，從 ping hello hello 桌面的電腦 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e98c5-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="e98c5-163">您應該測試連線 tooboth hello IP 位址指派 toohello 電腦，另一個用於 hello 網路連線，且 hello 其他 hello Azure 虛擬網路的 hello 電腦已連線到。</span><span class="sxs-lookup"><span data-stu-id="e98c5-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="e98c5-164">重複 hello 以及其他前端節點 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="e98c5-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="e98c5-165">步驟 4： 建立使用 Azure Toolkit 中的 hello HDInsight Tools for IntelliJ Spark Scala 應用程式，並將其設定為遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="e98c5-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="e98c5-166">啟動 IntelliJ IDEA，並建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="e98c5-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="e98c5-167">在 hello 新專案 對話方塊進行 hello 下列選項，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![建立 Spark Scala 應用程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="e98c5-169">從 hello 左窗格中，選取**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="e98c5-170">從 hello 右窗格中，選取**HDInsight (Scala) 上的 Spark**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="e98c5-171">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="e98c5-171">Click **Next**.</span></span>
2. <span data-ttu-id="e98c5-172">在 hello 下一步 視窗中，提供 hello 下列專案的詳細資料，然後再按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="e98c5-173">提供專案名稱和專案位置。</span><span class="sxs-lookup"><span data-stu-id="e98c5-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="e98c5-174">針對 [Project SDK] \(專案 SDK\)，Spark 2.x 叢集請使用 Java 1.8，Spark 1.x 叢集請使用 Java 1.7。</span><span class="sxs-lookup"><span data-stu-id="e98c5-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="e98c5-175">針對 [Spark Version] \(Spark 版本\)，Scala 專案建立精靈會為 Spark SDK 和 Scala SDK 整合正確的版本。</span><span class="sxs-lookup"><span data-stu-id="e98c5-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="e98c5-176">如果 hello spark 叢集的版本低 2.0，請選擇二手 1.x。</span><span class="sxs-lookup"><span data-stu-id="e98c5-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="e98c5-177">否則，您應該選取 Spark2.x。</span><span class="sxs-lookup"><span data-stu-id="e98c5-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="e98c5-178">此範例使用 Spark2.0.2(Scala 2.11.8)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="e98c5-179">![建立 Spark Scala 應用程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="e98c5-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="e98c5-180">hello Spark 專案會自動為您建立成品。</span><span class="sxs-lookup"><span data-stu-id="e98c5-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="e98c5-181">toosee hello 成品，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="e98c5-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="e98c5-182">從 hello**檔案**功能表上，按一下 **專案結構**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="e98c5-183">在 hello**專案結構**對話方塊中，按一下**成品**toosee hello 預設成品所建立。</span><span class="sxs-lookup"><span data-stu-id="e98c5-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="e98c5-184">![建立 JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="e98c5-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="e98c5-185">您也可以建立您自己的成品 bly 按一下 hello  **+** 圖示、 在 hello 圖中反白顯示。</span><span class="sxs-lookup"><span data-stu-id="e98c5-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="e98c5-186">加入程式庫 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="e98c5-186">Add libraries tooyour project.</span></span> <span data-ttu-id="e98c5-187">tooadd 文件庫，在 hello 專案樹狀目錄中的 hello 專案名稱上按一下滑鼠右鍵，然後按一下**開啟模組設定**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="e98c5-188">在 hello**專案結構**對話方塊中的，從 hello 左窗格中，按一下**文件庫**，按一下 hello （+） 符號，然後按一下**從 Maven**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![新增程式庫](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="e98c5-190">在 hello**從 Maven 儲存機制下載的程式庫**對話方塊方塊中，搜尋並新增下列程式庫的 hello。</span><span class="sxs-lookup"><span data-stu-id="e98c5-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="e98c5-191">複製`yarn-site.xml`和`core-site.xml`hello 從叢集前端節點，並將它 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="e98c5-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="e98c5-192">使用下列命令 toocopy hello 檔案 hello。</span><span class="sxs-lookup"><span data-stu-id="e98c5-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="e98c5-193">您可以使用[Cygwin](https://cygwin.com/install.html) toorun hello 下列`scp`命令從 hello 叢集 headnodes toocopy hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e98c5-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="e98c5-194">因為我們已加入 hello 叢集前端節點 IP 位址和主機名稱 fo hello hosts 檔案 hello 桌面上，我們可以使用 hello **scp** hello 下列方式中的命令。</span><span class="sxs-lookup"><span data-stu-id="e98c5-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="e98c5-195">新增這些檔案 tooyour 專案並將其複製下 hello **/src**資料夾中您專案的樹狀目錄，例如`<your project directory>\src`。</span><span class="sxs-lookup"><span data-stu-id="e98c5-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="e98c5-196">更新 hello `core-site.xml` toomake hello 下列變更。</span><span class="sxs-lookup"><span data-stu-id="e98c5-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="e98c5-197">`core-site.xml`包含加密的 hello hello 叢集相關聯的金鑰 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e98c5-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="e98c5-198">在 hello`core-site.xml`您加入 toohello 專案中，取代 hello 加密金鑰與 hello hello 預設儲存體帳戶相關聯的實際儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="e98c5-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="e98c5-199">請參閱 [管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="e98c5-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="e98c5-200">移除下列項目從 hello hello `core-site.xml`。</span><span class="sxs-lookup"><span data-stu-id="e98c5-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="e98c5-201">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e98c5-201">Save hello file.</span></span>
7. <span data-ttu-id="e98c5-202">加入您的應用程式的 hello 主要類別。</span><span class="sxs-lookup"><span data-stu-id="e98c5-202">Add hello Main class for your application.</span></span> <span data-ttu-id="e98c5-203">從 hello**專案總管**，以滑鼠右鍵按一下**src**，點太**新增**，然後按一下 **Scala 類別**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![新增原始程式碼](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="e98c5-205">在 hello**建立類別的新 Scala**對話方塊方塊中，提供名稱，如**種類**選取**物件**，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![新增原始程式碼](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="e98c5-207">在 hello`MyClusterAppMain.scala`檔案中，貼上下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="e98c5-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="e98c5-208">此程式碼會建立 hello Spark 內容，並啟動`executeJob`方法從 hello`SparkSample`物件。</span><span class="sxs-lookup"><span data-stu-id="e98c5-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="e98c5-209">重複步驟 8 和 9 tooadd 呼叫新的 Scala 物件上方`SparkSample`。</span><span class="sxs-lookup"><span data-stu-id="e98c5-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="e98c5-210">toothis 類別新增下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="e98c5-210">toothis class add hello following code.</span></span> <span data-ttu-id="e98c5-211">此程式碼，讀取 hello hello HVAC.csv （可在所有的 HDInsight Spark 叢集上）、 擷取 hello hello hello CSV 中的第七個資料行中只有一個數字的資料列和 hello 會將輸出寫入太**/HVACOut**下 hello 預設hello 叢集的儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="e98c5-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="e98c5-212">重複步驟 8 和 9 以上 tooadd 新的類別稱為 「 `RemoteClusterDebugging`。</span><span class="sxs-lookup"><span data-stu-id="e98c5-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="e98c5-213">這個類別會實作用於偵錯應用程式的 hello Spark 測試架構。</span><span class="sxs-lookup"><span data-stu-id="e98c5-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="e98c5-214">新增下列程式碼 toohello hello`RemoteClusterDebugging`類別。</span><span class="sxs-lookup"><span data-stu-id="e98c5-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="e98c5-215">幾個重要事項 toonote 這裡：</span><span class="sxs-lookup"><span data-stu-id="e98c5-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="e98c5-216">如`.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`，請確定 hello Spark 組件 JAR hello 叢集存放裝置 hello 指定路徑上，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="e98c5-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="e98c5-217">如`setJars`，指定將會建立 hello 成品 jar hello 位置。</span><span class="sxs-lookup"><span data-stu-id="e98c5-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="e98c5-218">通常是 `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`。</span><span class="sxs-lookup"><span data-stu-id="e98c5-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="e98c5-219">在 hello`RemoteClusterDebugging`類別，以滑鼠右鍵按一下 hello`test`關鍵字，然後選取**建立 RemoteClusterDebugging 組態**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="e98c5-221">在 [hello] 對話方塊中，請在提供 hello 組態的名稱，然後選取 hello**測試種類**為**測試名稱**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="e98c5-222">對於所有其他值保留預設值，按一下 套用，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="e98c5-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="e98c5-224">您現在應該會看到**遠端執行**組態 hello 功能表列中的下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="e98c5-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="e98c5-226">步驟 5： 偵錯模式執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e98c5-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="e98c5-227">在 IntelliJ 概念專案中，開啟`SparkSample.scala`並建立中斷點 下一步 too'val rdd1'。</span><span class="sxs-lookup"><span data-stu-id="e98c5-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="e98c5-228">在建立中斷點 hello 快顯功能表中選取**列在函式 executeJob**。</span><span class="sxs-lookup"><span data-stu-id="e98c5-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![新增中斷點](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="e98c5-230">按一下 hello**偵錯執行**按鈕的下一個 toohello**遠端執行**組態下拉式清單 toostart 執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e98c5-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="e98c5-232">當執行 hello 程式到達 hello 中斷點時，您應該會看到**偵錯工具**hello 下方窗格中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e98c5-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="e98c5-234">按一下 hello (**+**) 圖示 tooadd 監看式 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="e98c5-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="e98c5-236">此處，因為 hello 應用程式中斷之前 hello 變數`rdd1`使用所建立，我們可以看到什麼是 hello hello 變數中的第一次 5 個資料列此監看式`rdd`。</span><span class="sxs-lookup"><span data-stu-id="e98c5-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="e98c5-237">按 **ENTER**鍵。</span><span class="sxs-lookup"><span data-stu-id="e98c5-237">Press **ENTER**.</span></span>

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="e98c5-239">上述的 hello 映像中看到的內容是在執行階段，您可以查詢資料與偵錯的 terrabytes 如何您的應用程式進行時。</span><span class="sxs-lookup"><span data-stu-id="e98c5-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="e98c5-240">例如，在 hello hello 圖所示的輸出，您可以看到該 hello hello 輸出的第一個資料列是標頭。</span><span class="sxs-lookup"><span data-stu-id="e98c5-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="e98c5-241">有鑑於此，您可以修改您應用程式程式碼 tooskip hello 標頭資料列有必要。</span><span class="sxs-lookup"><span data-stu-id="e98c5-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="e98c5-242">您現在可以按一下 hello**繼續程式**圖示 tooproceed 與執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="e98c5-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="e98c5-244">如果順利完成 hello 應用程式，您應該會看到類似 hello 下列輸出。</span><span class="sxs-lookup"><span data-stu-id="e98c5-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![在 偵錯模式中執行 hello 程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="e98c5-246"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="e98c5-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="e98c5-247">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="e98c5-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="e98c5-248">示範</span><span class="sxs-lookup"><span data-stu-id="e98c5-248">Demo</span></span>
* <span data-ttu-id="e98c5-249">建立 Scala 專案 (影片)：[建立 Spark Scala 應用程式](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) \(Create Spark Scala Applications\)</span><span class="sxs-lookup"><span data-stu-id="e98c5-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="e98c5-250">遠端偵錯 （影片）：[使用 Azure Toolkit for IntelliJ toodebug Spark 應用程式，從遠端在 HDInsight 叢集上](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e98c5-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="e98c5-251">案例</span><span class="sxs-lookup"><span data-stu-id="e98c5-251">Scenarios</span></span>
* [<span data-ttu-id="e98c5-252">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="e98c5-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e98c5-253">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="e98c5-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e98c5-254">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="e98c5-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e98c5-255">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="e98c5-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e98c5-256">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="e98c5-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e98c5-257">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="e98c5-257">Create and run applications</span></span>
* [<span data-ttu-id="e98c5-258">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="e98c5-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e98c5-259">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="e98c5-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e98c5-260">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="e98c5-260">Tools and extensions</span></span>
* [<span data-ttu-id="e98c5-261">在 Azure Toolkit HDInsight Tools 用於 IntelliJ toocreate 並提交 Spark Scala 個應用程式</span><span class="sxs-lookup"><span data-stu-id="e98c5-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e98c5-262">透過 SSH 遠端 IntelliJ toodebug Spark 應用程式使用 Azure Toolkit</span><span class="sxs-lookup"><span data-stu-id="e98c5-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="e98c5-263">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="e98c5-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="e98c5-264">在 Azure Toolkit for Eclipse toocreate Spark 應用程式中使用 HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="e98c5-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="e98c5-265">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="e98c5-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e98c5-266">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="e98c5-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e98c5-267">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="e98c5-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e98c5-268">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="e98c5-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e98c5-269">管理資源</span><span class="sxs-lookup"><span data-stu-id="e98c5-269">Manage resources</span></span>
* [<span data-ttu-id="e98c5-270">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="e98c5-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e98c5-271">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="e98c5-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
