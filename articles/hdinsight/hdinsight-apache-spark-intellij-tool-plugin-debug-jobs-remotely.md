---
title: "適用於 IntelliJ 的 Azure 工具組 - 在 HDInsight Spark 上遠端偵錯應用程式 | Microsoft Docs"
description: "了解如何使用適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具，透過 VPN 對 HDInsight Spark 叢集上執行的應用程式進行遠端偵錯。"
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
ms.openlocfilehash: 5ce282aac94d0f22ea587cbe4005819310e23b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-debug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="2fcf7-103">使用適用於 IntelliJ 的 Azure 工具組，透過 VPN 在 HDInsight Spark 上對應用程式進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="2fcf7-103">Use Azure Toolkit for IntelliJ to debug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="2fcf7-104">透過 SSH 對 Spark 應用程式進行遠端偵錯是建議的方式。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-104">We recommend the way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="2fcf7-105">如需指示，請參閱[使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="2fcf7-106">本文提供如何使用適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具，來提交 HDInsight Spark 叢集上的 Spark 作業，然後從桌上型電腦遠端偵錯的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="2fcf7-107">若要這樣做，您必須執行下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="2fcf7-107">To do so, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="2fcf7-108">建立站對站或點對站 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="2fcf7-109">本文件中的步驟假設您使用站對站網路。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-109">The steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="2fcf7-110">在 Azure HDInsight 中建立 Spark 叢集是站對站 Azure 虛擬網路的一部分。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-110">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="2fcf7-111">請確認叢集前端節點與您的桌上型電腦之間的連線。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-111">Verify the connectivity between the cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="2fcf7-112">在 IntelliJ IDEA 中建立 Scala 應用程式，並設定它以進行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="2fcf7-113">執行和偵錯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-113">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fcf7-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="2fcf7-114">Prerequisites</span></span>
* <span data-ttu-id="2fcf7-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-115">An Azure subscription.</span></span> <span data-ttu-id="2fcf7-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="2fcf7-117">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="2fcf7-118">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="2fcf7-119">Oracle Java Development Kit。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-119">Oracle Java Development kit.</span></span> <span data-ttu-id="2fcf7-120">您可以從 [這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)加以安裝。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="2fcf7-121">IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-121">IntelliJ IDEA.</span></span> <span data-ttu-id="2fcf7-122">本文章使用 2017.1 版。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-122">This article uses version 2017.1.</span></span> <span data-ttu-id="2fcf7-123">您可以從[這裡](https://www.jetbrains.com/idea/download/)安裝它。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="2fcf7-124">適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="2fcf7-125">適用於 IntelliJ 的 HDInsight 工具是適用於 IntelliJ 的 Azure 工具組的一部分。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-125">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="2fcf7-126">如需有關如何安裝 Azure 工具組的指示，請參閱 [安裝 Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-126">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="2fcf7-127">從 IntelliJ IDEA 登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="2fcf7-128">請遵循 [這裡](hdinsight-apache-spark-intellij-tool-plugin.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-128">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="2fcf7-129">在 Windows 電腦上執行 Spark Scala 應用程式以進行遠端偵錯時，可能會發生 [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) 中所述的例外狀況，此例外狀況發生的原因是因為 Windows 上缺少 WinUtils.exe。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="2fcf7-130">若要解決這個錯誤，您必須[從這裡下載可執行檔](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe)，並將其放至 **C:\WinUtils\bin** 之類的位置。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-130">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="2fcf7-131">然後，您必須新增環境變數 **HADOOP_HOME**，並將變數的值設為 **C\WinUtils**。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-131">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="2fcf7-132">步驟 1：建立 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="2fcf7-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="2fcf7-133">請依照下列連結的指示建立 Azure 虛擬網路，然後確認桌上型電腦和 Azure 虛擬網路之間的連線。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-133">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="2fcf7-134">使用 Azure 入口網站建立具有站對站 VPN 連線的 VNet</span><span class="sxs-lookup"><span data-stu-id="2fcf7-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="2fcf7-135">使用 PowerShell 建立具有站對站 VPN 連線的 VNet</span><span class="sxs-lookup"><span data-stu-id="2fcf7-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="2fcf7-136">使用 PowerShell 設定虛擬網路的點對站連線</span><span class="sxs-lookup"><span data-stu-id="2fcf7-136">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="2fcf7-137">步驟 2：建立 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="2fcf7-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="2fcf7-138">您也應該在 Azure HDInsight 上建立 Apache Spark 叢集，這是您建立的 Azure 虛擬網路的一部分。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span></span> <span data-ttu-id="2fcf7-139">使用可於 [在 HDInsight 中建立以 Linux 為基礎的叢集](hdinsight-hadoop-provision-linux-clusters.md)取得的資訊。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-139">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="2fcf7-140">做為選擇性組態的一部分，選取您在上一個步驟中建立的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-140">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a><span data-ttu-id="2fcf7-141">步驟 3：請確認叢集前端節點與您的桌上型電腦之間的連線</span><span class="sxs-lookup"><span data-stu-id="2fcf7-141">Step 3: Verify the connectivity between the cluster headnode and your desktop</span></span>
1. <span data-ttu-id="2fcf7-142">取得前端節點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-142">Get the IP address of the headnode.</span></span> <span data-ttu-id="2fcf7-143">開啟叢集的 Ambari UI。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-143">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="2fcf7-144">從叢集刀鋒視窗中，按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-144">From the cluster blade, click **Dashboard**.</span></span>

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="2fcf7-146">從 Ambari UI 的右上角，按一下 [主機] 。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-146">From the Ambari UI, from the top-right corner, click **Hosts**.</span></span>

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="2fcf7-148">您應該會看到前端節點、背景工作角色節點和 zookeeper 節點的清單。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="2fcf7-149">前端節點有 **hn*** 前置詞。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-149">The headnodes have the **hn*** prefix.</span></span> <span data-ttu-id="2fcf7-150">按一下第一個前端節點。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-150">Click the first headnode.</span></span>

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="2fcf7-152">在開啟的頁面底部，從 [摘要]  方塊複製前端節點的 IP 位址和主機名稱。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-152">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span></span>

    ![尋找前端節點 IP](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="2fcf7-154">包含前端節點的 IP 位址和主機名稱，到您想要從中執行和遠端偵錯 Spark 作業的電腦上的 **主機** 檔案。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-154">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span></span> <span data-ttu-id="2fcf7-155">這可讓您使用 IP 位址和主機名稱，與前端節點通訊。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-155">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span></span>

   1. <span data-ttu-id="2fcf7-156">以提高的權限開啟 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="2fcf7-157">從 [檔案] 功能表中，按一下 [開啟]  然後瀏覽至主機檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-157">From the file menu, click **Open** and then navigate to the location of the hosts file.</span></span> <span data-ttu-id="2fcf7-158">在 Windows 電腦上，是 `C:\Windows\System32\Drivers\etc\hosts`。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="2fcf7-159">將下列項目新增至 **主機** 檔案。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-159">Add the following to the **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="2fcf7-160">從您連接到 HDInsight 叢集使用之 Azure 虛擬網路的電腦，確認您可以使用 IP 位址和主機名稱 ping 兩個前端節點。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-160">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span></span>
7. <span data-ttu-id="2fcf7-161">利用 [使用 SSH 連線到 HDInsight 叢集](hdinsight-hadoop-linux-use-ssh-unix.md)中的指示，將 SSH 連線至叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-161">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="2fcf7-162">從叢集前端節點，ping 桌上型電腦的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-162">From the cluster headnode, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="2fcf7-163">您應該測試指派至電腦的這兩個 IP 位址的連線能力，一個用於網路連接，而另一個則用於電腦連接的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-163">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span></span>
8. <span data-ttu-id="2fcf7-164">對其他前端節點重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-164">Repeat the steps for the other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="2fcf7-165">步驟 4：使用適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具來建立 Spark Scala 應用程式，並設定它以進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="2fcf7-165">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="2fcf7-166">啟動 IntelliJ IDEA，並建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="2fcf7-167">在新增專案對話方塊中選取下列選項，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-167">In the new project dialog box, make the following choices, and then click **Next**.</span></span>

    ![建立 Spark Scala 應用程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="2fcf7-169">從左窗格中，選取 [HDInsight] 。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-169">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="2fcf7-170">從右窗格中，選取 [HDInsight 上的 Spark (Scala)] 。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-170">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="2fcf7-171">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-171">Click **Next**.</span></span>
2. <span data-ttu-id="2fcf7-172">在下一個視窗中，提供下列專案詳細資料，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-172">In the next window, provide the following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="2fcf7-173">提供專案名稱和專案位置。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="2fcf7-174">針對 [Project SDK] \(專案 SDK\)，Spark 2.x 叢集請使用 Java 1.8，Spark 1.x 叢集請使用 Java 1.7。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="2fcf7-175">針對 [Spark Version] \(Spark 版本\)，Scala 專案建立精靈會為 Spark SDK 和 Scala SDK 整合正確的版本。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="2fcf7-176">如果 Spark 叢集版本低於 2.0，請選擇 Spark 1.x。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-176">If the spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="2fcf7-177">否則，您應該選取 Spark2.x。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="2fcf7-178">此範例使用 Spark2.0.2(Scala 2.11.8)。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="2fcf7-179">![建立 Spark Scala 應用程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="2fcf7-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="2fcf7-180">Spark 專案會自動為您建立構件。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-180">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="2fcf7-181">若要查看構件，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-181">To see the artifact, follow these steps.</span></span>

   1. <span data-ttu-id="2fcf7-182">在 [檔案] 功能表中，按一下 [專案結構]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-182">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="2fcf7-183">在 [專案結構] 對話方塊中，按一下 [構件]，以查看建立的預設構件。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-183">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
   <span data-ttu-id="2fcf7-184">![建立 JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="2fcf7-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="2fcf7-185">您也可以建立自己的構件，方法是按一下上圖中強調顯示的 [+] **+** 圖示。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-185">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>

4. <span data-ttu-id="2fcf7-186">將程式庫新增至專案。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-186">Add libraries to your project.</span></span> <span data-ttu-id="2fcf7-187">若要新增程式庫，以滑鼠右鍵按一下專案樹狀結構中的專案名稱，然後按一下 [Open Module Settings (開啟模組設定)] 。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-187">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="2fcf7-188">在 [專案結構] 對話方塊中，從左窗格中按一下 [程式庫]，按一下 (+) 符號，然後按一下 [從 Maven]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-188">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span></span>

    ![新增程式庫](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="2fcf7-190">在 [Download Library from Maven Repository (從 Maven 儲存機制下載程式庫)]  對話方塊中，搜尋並新增下列程式庫。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-190">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="2fcf7-191">從叢集前端節點複製 `yarn-site.xml` 和 `core-site.xml`，並將它新增至專案。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-191">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span></span> <span data-ttu-id="2fcf7-192">使用下列命令來複製檔案。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-192">Use the following commands to copy the files.</span></span> <span data-ttu-id="2fcf7-193">您可以使用 [Cygwin](https://cygwin.com/install.html) 以執行下列 `scp` 命令，從叢集前端節點複製檔案。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-193">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="2fcf7-194">因為我們已經將叢集前端節點 IP 位址及主機名稱新增至桌上型電腦的主機檔案，因此可以下列方式使用 **scp** 命令。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-194">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="2fcf7-195">在您專案樹狀結構的 **/src** 資料夾下複製這些檔案，以將它們新增至專案，例如 `<your project directory>\src`。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-195">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="2fcf7-196">更新 `core-site.xml` 以進行下列變更。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-196">Update the `core-site.xml` to make the following changes.</span></span>

   1. <span data-ttu-id="2fcf7-197">`core-site.xml` 包含與叢集相關聯的儲存體帳戶的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-197">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="2fcf7-198">在您新增至專案的 `core-site.xml` 中，以與預設儲存體帳戶相關聯的實際儲存體金鑰取代加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-198">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="2fcf7-199">請參閱 [管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="2fcf7-200">從 `core-site.xml`移除下列項目。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-200">Remove the following entries from the `core-site.xml`.</span></span>

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
   3. <span data-ttu-id="2fcf7-201">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-201">Save the file.</span></span>
7. <span data-ttu-id="2fcf7-202">新增您應用程式的主要類別。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-202">Add the Main class for your application.</span></span> <span data-ttu-id="2fcf7-203">從 [專案總管] 中，以滑鼠右鍵按一下 [src]、指向 [新增]，然後按一下 [Scala 類別]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-203">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>

    ![新增原始程式碼](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="2fcf7-205">在 [建立新的 Scala 類別] 對話方塊中，提供一個名稱，並針對 [種類] 選取 [物件]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-205">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![新增原始程式碼](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="2fcf7-207">在 `MyClusterAppMain.scala` 檔案中，貼上下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-207">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="2fcf7-208">此程式碼會建立 Spark 內容，並且從 `SparkSample` 物件啟動 `executeJob` 方法。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-208">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span></span>

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

10. <span data-ttu-id="2fcf7-209">重複上述的步驟 8 和 9，以新增稱為 `SparkSample`的新 Scala 物件。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-209">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="2fcf7-210">對這個類別新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-210">To this class add the following code.</span></span> <span data-ttu-id="2fcf7-211">此程式碼會從 HVAC.csv (所有 HDInsight Spark 叢集上均有提供) 讀取資料、擷取在 CSV 的第七個資料行中只有個位數的資料列，並將輸出寫入到叢集預設儲存體容器下的 **/HVACOut** 。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-211">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="2fcf7-212">重複上述的步驟 8 和 9，以新增稱為 `RemoteClusterDebugging`的新類別。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-212">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="2fcf7-213">這個類別會實作 Spark 測試架構，用於偵錯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-213">This class implements the Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="2fcf7-214">將下列程式碼新增至 `RemoteClusterDebugging` 類別。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-214">Add the following code to the `RemoteClusterDebugging` class.</span></span>

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

     <span data-ttu-id="2fcf7-215">這裡有幾個重點值得注意：</span><span class="sxs-lookup"><span data-stu-id="2fcf7-215">Couple of important things to note here:</span></span>

   * <span data-ttu-id="2fcf7-216">對於 `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`，請確定 Spark 組件 JAR 可用於位於指定路徑的叢集存放區。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
   * <span data-ttu-id="2fcf7-217">對於 `setJars`，指定將會建立構件 jar 的位置。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-217">For `setJars`, specify the location where the artifact jar will be created.</span></span> <span data-ttu-id="2fcf7-218">通常是 `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="2fcf7-219">在 `RemoteClusterDebugging` 類別中，以滑鼠右鍵按一下 `test` 關鍵字，然後選取 [建立 RemoteClusterDebugging 組態]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-219">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="2fcf7-221">在對話方塊中，提供組態的名稱，然後選取 [測試種類] 做為 [測試名稱]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-221">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span></span> <span data-ttu-id="2fcf7-222">對於所有其他值保留預設值，按一下 [套用]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="2fcf7-224">您現在應該會在功能表列中看到 [Remote Run (遠端執行)]  組態下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-224">You should now see a **Remote Run** configuration drop-down in the menu bar.</span></span>

    ![建立遠端組態](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="2fcf7-226">步驟 5：在偵錯模式中執行應用程式</span><span class="sxs-lookup"><span data-stu-id="2fcf7-226">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="2fcf7-227">在您的 IntelliJ IDEA 專案中，開啟 `SparkSample.scala` 並且在 'val rdd1' 旁邊建立中斷點。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span></span> <span data-ttu-id="2fcf7-228">在建立中斷點的快顯功能表中，選取 **executeJob 函數中的一行**。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-228">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![新增中斷點](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="2fcf7-230">按一下 [遠端執行] 組態下拉式清單旁的 [偵錯執行] 按鈕，開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-230">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span></span>

    ![在偵錯模式中執行程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="2fcf7-232">當程式執行觸達中斷點時，您應該會在下方窗格中看到 [Debugger (偵錯工具)]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-232">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span></span>

    ![在偵錯模式中執行程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="2fcf7-234">按一下 (**+**) 圖示，以新增監看式，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-234">Click the (**+**) icon to add a watch as shown in the image below.</span></span>

    ![在偵錯模式中執行程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="2fcf7-236">這裡因為應用程式在建立變數 `rdd1` 之前中斷，我們可以使用此監看式看到變數 `rdd` 中的前 5 個資料列。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-236">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span></span> <span data-ttu-id="2fcf7-237">按 **ENTER**鍵。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-237">Press **ENTER**.</span></span>

    ![在偵錯模式中執行程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="2fcf7-239">您在上述映像中看到的內容是在執行階段，您可以查詢 terrabytes 的資料，並且針對應用程式的進度進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-239">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="2fcf7-240">例如，您可以在上述映像中顯示的輸出，看見輸出的第一個資料列是標頭。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-240">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="2fcf7-241">有鑑於此，您可以修改應用程式程式碼，視需要略過標頭資料列。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-241">Based on this, you can modify your application code to skip the header row if required.</span></span>
5. <span data-ttu-id="2fcf7-242">您現在可以按一下 [Resume Program (繼續程式)]  圖示，以繼續執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-242">You can now click the **Resume Program** icon to proceed with your application run.</span></span>

    ![在偵錯模式中執行程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="2fcf7-244">如果應用程式順利完成，應該會看到類似下列的輸出。</span><span class="sxs-lookup"><span data-stu-id="2fcf7-244">If the application completes successfully, you should see an output like the following.</span></span>

    ![在偵錯模式中執行程式](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="2fcf7-246"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="2fcf7-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="2fcf7-247">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="2fcf7-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="2fcf7-248">示範</span><span class="sxs-lookup"><span data-stu-id="2fcf7-248">Demo</span></span>
* <span data-ttu-id="2fcf7-249">建立 Scala 專案 (影片)：[建立 Spark Scala 應用程式](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) \(Create Spark Scala Applications\)</span><span class="sxs-lookup"><span data-stu-id="2fcf7-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="2fcf7-250">遠端偵錯 (影片)：[使用適用於 IntelliJ 的 Azure 工具組對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="2fcf7-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="2fcf7-251">案例</span><span class="sxs-lookup"><span data-stu-id="2fcf7-251">Scenarios</span></span>
* [<span data-ttu-id="2fcf7-252">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="2fcf7-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2fcf7-253">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="2fcf7-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="2fcf7-254">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="2fcf7-254">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2fcf7-255">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="2fcf7-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="2fcf7-256">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="2fcf7-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="2fcf7-257">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="2fcf7-257">Create and run applications</span></span>
* [<span data-ttu-id="2fcf7-258">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="2fcf7-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2fcf7-259">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="2fcf7-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="2fcf7-260">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="2fcf7-260">Tools and extensions</span></span>
* [<span data-ttu-id="2fcf7-261">使用適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具建立和提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="2fcf7-261">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="2fcf7-262">使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 Spark 應用程式進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="2fcf7-262">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="2fcf7-263">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="2fcf7-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="2fcf7-264">使用適用於 Eclipse 的 Azure 工具組中的 HDInsight 工具建立 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="2fcf7-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="2fcf7-265">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="2fcf7-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="2fcf7-266">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="2fcf7-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="2fcf7-267">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="2fcf7-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="2fcf7-268">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="2fcf7-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="2fcf7-269">管理資源</span><span class="sxs-lookup"><span data-stu-id="2fcf7-269">Manage resources</span></span>
* [<span data-ttu-id="2fcf7-270">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="2fcf7-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="2fcf7-271">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="2fcf7-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
