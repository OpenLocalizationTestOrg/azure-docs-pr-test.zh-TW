---
title: "搭配 Windows 型 Azure HDInsight 使用 Apache Phoenix 和 SQuirreL | Microsoft Docs"
description: "了解如何使用 HDinsight 中的 Apache Phoenix，以及如何在您的工作站上安裝與設定 SQuirreL 以連線到 HDInsight 中的 HBase 叢集。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 024b70df99fdefa1598225ebb1fbfee85ea375d0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="f0516-103">在 HDInsight 中搭配 Windows 型 HBase 叢集使用 Apache Phoenix 和 SQuirreL</span><span class="sxs-lookup"><span data-stu-id="f0516-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="f0516-104">了解如何使用 HDinsight 中的 [Apache Phoenix](http://phoenix.apache.org/) ，以及如何在您的工作站上安裝與設定 SQuirreL 以連線到 HDInsight 中的 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="f0516-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span></span> <span data-ttu-id="f0516-105">如需有關 Phoenix 的詳細資訊，請參閱 [15 分鐘內了解 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)。</span><span class="sxs-lookup"><span data-stu-id="f0516-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="f0516-106">如需 Phoenix 文法，請參閱 [Phoenix 文法](http://phoenix.apache.org/language/index.html)。</span><span class="sxs-lookup"><span data-stu-id="f0516-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="f0516-107">如需 HDInsight 中的 Phoenix 版本資訊，請參閱 [HDInsight 在 Hadoop 叢集版本中提供什麼新功能？](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="f0516-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="f0516-108">本文件的步驟只適用於 Windows 型 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f0516-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="f0516-109">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="f0516-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="f0516-110">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="f0516-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f0516-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="f0516-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="f0516-112">如需在 Linux 型 HDInsight 上使用 Phoenix 的相關資訊，請參閱[在 HDinsight 中搭配 Linux 型 HBase 叢集使用 Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f0516-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="f0516-113">使用 SQLLine</span><span class="sxs-lookup"><span data-stu-id="f0516-113">Use SQLLine</span></span>
<span data-ttu-id="f0516-114">[SQLLine](http://sqlline.sourceforge.net/) 是執行 SQL 的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="f0516-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f0516-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="f0516-115">Prerequisites</span></span>
<span data-ttu-id="f0516-116">開始使用 SQLLine 之前，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="f0516-116">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="f0516-117">**HDInsight 中的 HBase 叢集**。</span><span class="sxs-lookup"><span data-stu-id="f0516-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="f0516-118">如需有關佈建 HBase 叢集的資訊，請參閱[開始使用 HDInsight 中的 Apache HBase][hdinsight-hbase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="f0516-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="f0516-119">**透過遠端桌面通訊協定連接到 HBase 叢集**。</span><span class="sxs-lookup"><span data-stu-id="f0516-119">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="f0516-120">如需相關指示，請參閱[使用 Azure 傳統入口網站管理 HDInsight 中的 Hadoop 叢集][hdinsight-manage-portal]。</span><span class="sxs-lookup"><span data-stu-id="f0516-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="f0516-121">**找出主機名稱**</span><span class="sxs-lookup"><span data-stu-id="f0516-121">**To find out the host name**</span></span>

1. <span data-ttu-id="f0516-122">從桌面開啟 **Hadoop 命令列** 。</span><span class="sxs-lookup"><span data-stu-id="f0516-122">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="f0516-123">執行下列命令以取得 DNS 尾碼：</span><span class="sxs-lookup"><span data-stu-id="f0516-123">Run the following command to get the DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="f0516-124">並記下 **連線專用 DNS 尾碼**。</span><span class="sxs-lookup"><span data-stu-id="f0516-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="f0516-125">例如， *myhbasecluster.f5.internal.cloudapp.net*。</span><span class="sxs-lookup"><span data-stu-id="f0516-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="f0516-126">當您連線至 HBase 叢集時，您必須使用 FQDN 連線到其中一個 Zookeeper。</span><span class="sxs-lookup"><span data-stu-id="f0516-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span></span> <span data-ttu-id="f0516-127">每個 HDInsight 叢集有 3 個 Zookeeper。</span><span class="sxs-lookup"><span data-stu-id="f0516-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="f0516-128">它們是 *zookeeper0*、*zookeeper1* 和 *zookeeper2*。</span><span class="sxs-lookup"><span data-stu-id="f0516-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="f0516-129">FQDN 看起來像是 *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*。</span><span class="sxs-lookup"><span data-stu-id="f0516-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="f0516-130">**使用 SQLLine**</span><span class="sxs-lookup"><span data-stu-id="f0516-130">**To use SQLLine**</span></span>

1. <span data-ttu-id="f0516-131">從桌面開啟 **Hadoop 命令列** 。</span><span class="sxs-lookup"><span data-stu-id="f0516-131">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="f0516-132">執行下列命令來開啟 SQLLine：</span><span class="sxs-lookup"><span data-stu-id="f0516-132">Run the following commands to open SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [The FQDN of one of the Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="f0516-134">此範例中使用的命令：</span><span class="sxs-lookup"><span data-stu-id="f0516-134">The commands used in the sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="f0516-135">如需詳細資訊，請參閱 [SQLLine 手冊](http://sqlline.sourceforge.net/#manual)和 [Phoenix 文法](http://phoenix.apache.org/language/index.html)。</span><span class="sxs-lookup"><span data-stu-id="f0516-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="f0516-136">使用 SQuirreL</span><span class="sxs-lookup"><span data-stu-id="f0516-136">Use SQuirreL</span></span>
<span data-ttu-id="f0516-137">[SQuirrel SQL 用戶端](http://squirrel-sql.sourceforge.net/)是圖形化 Java 程式，可讓您檢視 JDBC 相容資料庫的結構、瀏覽資料表中的資料，並發出 SQL 命令等等。它可以用來連接到 HDInsight 上的 Apache Phoenix。</span><span class="sxs-lookup"><span data-stu-id="f0516-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span></span>

<span data-ttu-id="f0516-138">本結說明如在您的工作站上安裝與設定 SQuirreL 以透過 VPN 連線到 HDInsight 中的 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="f0516-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f0516-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="f0516-139">Prerequisites</span></span>
<span data-ttu-id="f0516-140">遵循程序之前，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="f0516-140">Before following the procedures, you must have the following:</span></span>

* <span data-ttu-id="f0516-141">將 HBase 叢集部署至具備 DNS 虛擬機器的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f0516-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="f0516-142">如需相關指示，請參閱[在 Azure 虛擬網路上建立 HBase 叢集][hdinsight-hbase-provision-vnet]。</span><span class="sxs-lookup"><span data-stu-id="f0516-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="f0516-143">取得 HBase 叢集的連線專用 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="f0516-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="f0516-144">若要取得該尾碼，請 RDP 到叢集，然後執行 IPConfig。</span><span class="sxs-lookup"><span data-stu-id="f0516-144">To get it, RDP into the cluster, and then run IPConfig.</span></span>  <span data-ttu-id="f0516-145">DNS 尾碼會類似於：</span><span class="sxs-lookup"><span data-stu-id="f0516-145">The DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="f0516-146">在您的工作站上下載並安裝 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="f0516-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="f0516-147">您將需要封裝的 makecert 以建立您的憑證。</span><span class="sxs-lookup"><span data-stu-id="f0516-147">You will need makecert from the package to create your certificate.</span></span>  
* <span data-ttu-id="f0516-148">在您的工作站上下載並安裝 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 。</span><span class="sxs-lookup"><span data-stu-id="f0516-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="f0516-149">SQuirreL SQL 用戶端 3.0 版和更新版本需要 JRE 1.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f0516-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-to-the-azure-virtual-network"></a><span data-ttu-id="f0516-150">設定點對站 VPN 連線到 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="f0516-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span></span>
<span data-ttu-id="f0516-151">設定點對站 VPN 連線包含 3 個步驟：</span><span class="sxs-lookup"><span data-stu-id="f0516-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="f0516-152">設定虛擬網路和動態路由閘道</span><span class="sxs-lookup"><span data-stu-id="f0516-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="f0516-153">建立您的憑證</span><span class="sxs-lookup"><span data-stu-id="f0516-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="f0516-154">設定 VPN 用戶端</span><span class="sxs-lookup"><span data-stu-id="f0516-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="f0516-155">如需詳細資訊，請參閱 [設定點對站 VPN 連線到 Azure 虛擬網路](../vpn-gateway/vpn-gateway-point-to-site-create.md) 。</span><span class="sxs-lookup"><span data-stu-id="f0516-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="f0516-156">設定虛擬網路和動態路由閘道</span><span class="sxs-lookup"><span data-stu-id="f0516-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="f0516-157">確保您已在 Azure 虛擬網路中佈建 HBase 叢集 (請參閱本節的必要條件)。</span><span class="sxs-lookup"><span data-stu-id="f0516-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span></span> <span data-ttu-id="f0516-158">下一步是設定點對站連線。</span><span class="sxs-lookup"><span data-stu-id="f0516-158">The next step is to configure a point-to-site connection.</span></span>

<span data-ttu-id="f0516-159">**設定點對站連線**</span><span class="sxs-lookup"><span data-stu-id="f0516-159">**To configure the point-to-site connectivity**</span></span>

1. <span data-ttu-id="f0516-160">登入 [Azure 傳統入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f0516-160">Sign in to the [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="f0516-161">在左側按一下 [ **網路**]。</span><span class="sxs-lookup"><span data-stu-id="f0516-161">On the left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="f0516-162">按一下您已建立的虛擬網路 (請參閱[在 Azure 虛擬網路上佈建 HBase 叢集][hdinsight-hbase-provision-vnet])。</span><span class="sxs-lookup"><span data-stu-id="f0516-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="f0516-163">按一下頂端的 [ **設定** ]。</span><span class="sxs-lookup"><span data-stu-id="f0516-163">Click **CONFIGURE** from the top.</span></span>
5. <span data-ttu-id="f0516-164">在 [點對站連線] 區段中，選取 [設定點對站連線]。</span><span class="sxs-lookup"><span data-stu-id="f0516-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="f0516-165">設定**起始 IP** 和 **CIDR** 來指定您的 VPN 用戶端在連線時接收 IP 位址的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="f0516-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="f0516-166">此範圍不能與任何位於內部部署網路及您將連線之 Azure 虛擬網路的範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="f0516-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="f0516-167">例如，</span><span class="sxs-lookup"><span data-stu-id="f0516-167">For example.</span></span> <span data-ttu-id="f0516-168">如果您選取 10.0.0.0/20 做為虛擬網路，您可以選取 10.1.0.0/24 做為用戶端的位址空間。</span><span class="sxs-lookup"><span data-stu-id="f0516-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span></span> <span data-ttu-id="f0516-169">如需詳細資訊，請參閱[點對站連線][vnet-point-to-site-connectivity]頁面。</span><span class="sxs-lookup"><span data-stu-id="f0516-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="f0516-170">在 [虛擬網路位址空間] 區段中，按一下 [ **新增閘道子網路**]。</span><span class="sxs-lookup"><span data-stu-id="f0516-170">In the virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="f0516-171">按一下頁面底部的 [ **儲存** ]。</span><span class="sxs-lookup"><span data-stu-id="f0516-171">Click **SAVE** on the bottom of the page.</span></span>
9. <span data-ttu-id="f0516-172">按一下 [ **是** ] 以確認變更。</span><span class="sxs-lookup"><span data-stu-id="f0516-172">Click **YES** to confirm the change.</span></span> <span data-ttu-id="f0516-173">請等候系統完成變更，才能繼續進行下一個程序。</span><span class="sxs-lookup"><span data-stu-id="f0516-173">Wait until the system has finished making the change before you proceed to the next procedure.</span></span>

<span data-ttu-id="f0516-174">**建立動態路由閘道**</span><span class="sxs-lookup"><span data-stu-id="f0516-174">**To create a dynamic routing gateway**</span></span>

1. <span data-ttu-id="f0516-175">從 Azure 傳統入口網站中，按一下頁面頂端的 [儀表板]  。</span><span class="sxs-lookup"><span data-stu-id="f0516-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span></span>
2. <span data-ttu-id="f0516-176">按一下頁面底部的 [ **建立閘道** ]。</span><span class="sxs-lookup"><span data-stu-id="f0516-176">Click **CREATE GATEWAY** from the bottom of the page.</span></span>
3. <span data-ttu-id="f0516-177">按一下 [ **是** ] 以確認。</span><span class="sxs-lookup"><span data-stu-id="f0516-177">Click **YES** to confirm.</span></span> <span data-ttu-id="f0516-178">請等候建立閘道。</span><span class="sxs-lookup"><span data-stu-id="f0516-178">Wait until the gateway is created.</span></span>
4. <span data-ttu-id="f0516-179">按一下頂端的 [ **儀表板** ]。</span><span class="sxs-lookup"><span data-stu-id="f0516-179">Click **DASHBOARD** from the top.</span></span>  <span data-ttu-id="f0516-180">您會看到虛擬網路的視覺化圖表：</span><span class="sxs-lookup"><span data-stu-id="f0516-180">You will see a visual diagram of the virtual network:</span></span>

    ![Azure 虛擬網路點對站虛擬圖表][img-vnet-diagram]

    <span data-ttu-id="f0516-182">此圖表顯示 0 個用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="f0516-182">The diagram shows 0 client connections.</span></span> <span data-ttu-id="f0516-183">建立虛擬網路的連線之後，此數字將會更新為一。</span><span class="sxs-lookup"><span data-stu-id="f0516-183">After you make a connection to the virtual network, the number will be updated to one.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="f0516-184">建立您的憑證</span><span class="sxs-lookup"><span data-stu-id="f0516-184">Create your certificates</span></span>
<span data-ttu-id="f0516-185">建立 X.509 憑證的其中一個方式是使用 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) 隨附的憑證建立工具 (makecert.exe)。</span><span class="sxs-lookup"><span data-stu-id="f0516-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="f0516-186">**建立自我簽署根憑證**</span><span class="sxs-lookup"><span data-stu-id="f0516-186">**To create a self-signed root certificate**</span></span>

1. <span data-ttu-id="f0516-187">從您的工作站，開啟命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="f0516-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="f0516-188">瀏覽至 [Visual Studio 工具] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f0516-188">Navigate to the Visual Studio tools folder.</span></span>
3. <span data-ttu-id="f0516-189">下面範例中的下列命令將在您工作站上的個人憑證存放區中建立與安裝根憑證，並建立您稍後將上傳至 Azure 傳統入口網站的相對應 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="f0516-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="f0516-190">將變更為您想要在其中放置 .cer 檔案的目錄，在該目錄中 HBaseVnetVPNRootCertificate 是您想要使用的憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="f0516-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span></span>

    <span data-ttu-id="f0516-191">不要關閉命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="f0516-191">Don't close the command prompt.</span></span>  <span data-ttu-id="f0516-192">您將在下一個程序中需要此提示字元。</span><span class="sxs-lookup"><span data-stu-id="f0516-192">You will need it in the next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f0516-193">因為您已經建立會產生用戶端憑證的根憑證，您可能會想要將此憑證及其私密金鑰匯出，並將它儲存到可復原的安全位置。</span><span class="sxs-lookup"><span data-stu-id="f0516-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="f0516-194">**建立用戶端憑證**</span><span class="sxs-lookup"><span data-stu-id="f0516-194">**To create a client certificate**</span></span>

* <span data-ttu-id="f0516-195">從相同的命令提示字元 (必須在您建立根憑證所在的相同電腦上。</span><span class="sxs-lookup"><span data-stu-id="f0516-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span></span> <span data-ttu-id="f0516-196">用戶端憑證必須從根憑證產生)，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f0516-196">The client certificate must be generated from the root certificate), run the following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="f0516-197">HBaseVnetVPNRootCertificate 是根憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="f0516-197">HBaseVnetVPNRootCertificate is the root certificate name.</span></span>  <span data-ttu-id="f0516-198">它必須符合根憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="f0516-198">It has to match the root certificate name.</span></span>  

    <span data-ttu-id="f0516-199">根憑證和用戶端憑證都會儲存在電腦上的個人憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="f0516-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="f0516-200">使用 certmgr.msc 來驗證。</span><span class="sxs-lookup"><span data-stu-id="f0516-200">Use certmgr.msc to verify.</span></span>

    ![Azure 虛擬網路點對站 VPN 憑證][img-certificate]

    <span data-ttu-id="f0516-202">您想要連接到虛擬網路的每一部電腦都必須安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="f0516-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="f0516-203">建議您最好針對要連接到虛擬網路的每部電腦建立唯一的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="f0516-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="f0516-204">若要匯出用戶端憑證，請使用 certmgr.msc。</span><span class="sxs-lookup"><span data-stu-id="f0516-204">To export the client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="f0516-205">**將根憑證上傳到 Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="f0516-205">**To upload the root certificate to the Azure Classic Portal**</span></span>

1. <span data-ttu-id="f0516-206">從 Azure 傳統入口網站，按一下左邊的 [網路]  。</span><span class="sxs-lookup"><span data-stu-id="f0516-206">From the Azure Classic Portal, click **NETWORK** on the left.</span></span>
2. <span data-ttu-id="f0516-207">按一下 HBase 叢集部署所在的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f0516-207">Click the virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="f0516-208">按一下頂端的 [ **憑證** ]。</span><span class="sxs-lookup"><span data-stu-id="f0516-208">Click **CERTIFICATES** from the top.</span></span>
4. <span data-ttu-id="f0516-209">按一下底部的 [ **上傳** ]，並指定您已在前一個程序中建立的根憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="f0516-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span></span> <span data-ttu-id="f0516-210">請等到憑證匯入。</span><span class="sxs-lookup"><span data-stu-id="f0516-210">Wait until the certificate got imported.</span></span>
5. <span data-ttu-id="f0516-211">按一下頂端的 [ **儀表板** ]。</span><span class="sxs-lookup"><span data-stu-id="f0516-211">Click **DASHBOARD** on the top.</span></span>  <span data-ttu-id="f0516-212">虛擬圖表會顯示狀態。</span><span class="sxs-lookup"><span data-stu-id="f0516-212">The virtual diagram shows the status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="f0516-213">設定 VPN 用戶端</span><span class="sxs-lookup"><span data-stu-id="f0516-213">Configure your VPN client</span></span>
<span data-ttu-id="f0516-214">**下載與安裝用戶端 VPN 封裝**</span><span class="sxs-lookup"><span data-stu-id="f0516-214">**To download and install the client VPN package**</span></span>

1. <span data-ttu-id="f0516-215">從快速瀏覽區段中虛擬網路的 [儀表板] 頁面，根據您的工作站 OS 版本按一下 [下載 64 位元用戶端 VPN 封裝] 或 [下載 32 位元用戶端 VPN 封裝]。</span><span class="sxs-lookup"><span data-stu-id="f0516-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="f0516-216">按一下 [ **執行** ] 以安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="f0516-216">Click **Run** to install the package.</span></span>
3. <span data-ttu-id="f0516-217">在安全性提示字元中，按一下 [更多資訊]，然後按一下 [仍要執行]。</span><span class="sxs-lookup"><span data-stu-id="f0516-217">At the security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="f0516-218">按兩下 [ **是** ]。</span><span class="sxs-lookup"><span data-stu-id="f0516-218">Click **Yes** twice.</span></span>

<span data-ttu-id="f0516-219">**連線到 VPN**</span><span class="sxs-lookup"><span data-stu-id="f0516-219">**To connect to VPN**</span></span>

1. <span data-ttu-id="f0516-220">在您的工作站桌面上，按一下工作列上的網路圖示。</span><span class="sxs-lookup"><span data-stu-id="f0516-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span></span> <span data-ttu-id="f0516-221">您會看到虛擬網路名稱的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="f0516-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="f0516-222">按一下 VPN 連線名稱。</span><span class="sxs-lookup"><span data-stu-id="f0516-222">Click the VPN connection name.</span></span>
3. <span data-ttu-id="f0516-223">按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="f0516-223">Click **Connect**.</span></span>

<span data-ttu-id="f0516-224">**測試 VPN 連線和網域名稱解析**</span><span class="sxs-lookup"><span data-stu-id="f0516-224">**To test the VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="f0516-225">若 HBase 叢集的 DNS 尾碼為 myhbase.b7.internal.cloudapp.net，請從工作站開啟命令提示字元，並且 ping 下列其中一個名稱：</span><span class="sxs-lookup"><span data-stu-id="f0516-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="f0516-226">安裝與設定您的工作站上的 SQuirreL</span><span class="sxs-lookup"><span data-stu-id="f0516-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="f0516-227">**安裝 SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="f0516-227">**To install SQuirreL**</span></span>

1. <span data-ttu-id="f0516-228">從 [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation)下載 SQuirrel SQL 用戶端 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="f0516-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="f0516-229">開啟/執行 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="f0516-229">Open/run the jar file.</span></span> <span data-ttu-id="f0516-230">它需要 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html)。</span><span class="sxs-lookup"><span data-stu-id="f0516-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="f0516-231">按兩下 [ **下一步** ]。</span><span class="sxs-lookup"><span data-stu-id="f0516-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="f0516-232">指定您具有寫入權限的路徑，然後按 [ **下一步**]。</span><span class="sxs-lookup"><span data-stu-id="f0516-232">Specify a path where you have the write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f0516-233">預設的安裝資料夾位於 C:\Program Files\squirrel sql 3.6 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f0516-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="f0516-234">若要寫入此路徑，必須將系統管理員權限授與安裝程式。</span><span class="sxs-lookup"><span data-stu-id="f0516-234">In order to write to this path, the installer must be granted the administrator privilege.</span></span> <span data-ttu-id="f0516-235">您可以系統管理員身分開啟命令提示字元、瀏覽至 Java 的 bin 資料夾，然後再執行：</span><span class="sxs-lookup"><span data-stu-id="f0516-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="f0516-236">java.exe-jar [SQuirreL jar 檔案的路徑]</span><span class="sxs-lookup"><span data-stu-id="f0516-236">java.exe -jar [the path of the SQuirreL jar file]</span></span>
5. <span data-ttu-id="f0516-237">按一下 [ **確定** ] 以確認建立目標目錄。</span><span class="sxs-lookup"><span data-stu-id="f0516-237">Click **OK** to confirm creating the target directory.</span></span>
6. <span data-ttu-id="f0516-238">預設設定是安裝基底和標準封裝。</span><span class="sxs-lookup"><span data-stu-id="f0516-238">The default setting is to install the Base and Standard packages.</span></span>  <span data-ttu-id="f0516-239">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f0516-239">Click **Next**.</span></span>
7. <span data-ttu-id="f0516-240">依序按兩下 [下一步] 和 [完成]。</span><span class="sxs-lookup"><span data-stu-id="f0516-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="f0516-241">**安裝 Phoenix 驅動程式**</span><span class="sxs-lookup"><span data-stu-id="f0516-241">**To install the Phoenix driver**</span></span>

<span data-ttu-id="f0516-242">Phoenix 驅動程式 jar 檔案位於 HBase 叢集上。</span><span class="sxs-lookup"><span data-stu-id="f0516-242">The phoenix driver jar file is located on the HBase cluster.</span></span> <span data-ttu-id="f0516-243">此路徑根據版本與下列項目相似：</span><span class="sxs-lookup"><span data-stu-id="f0516-243">The path is similar to the following based on the versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="f0516-244">您必須將它複製到您的工作站中的 [SQuirreL 安裝資料夾]/lib 路徑下。</span><span class="sxs-lookup"><span data-stu-id="f0516-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="f0516-245">最簡單的方法是 RDP 到叢集中，然後再使用檔案複製/貼上 (CTRL + C 和 CTRL + V 鍵)，將它複製到您的工作站。</span><span class="sxs-lookup"><span data-stu-id="f0516-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span></span>

<span data-ttu-id="f0516-246">**將 Phoenix 驅動程式新增至 SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="f0516-246">**To add a Phoenix driver to SQuirreL**</span></span>

1. <span data-ttu-id="f0516-247">從您的工作站開啟 SQuirreL SQL 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f0516-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="f0516-248">按一下左邊的 [ **驅動程式** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f0516-248">Click the **Driver** tab on the left.</span></span>
3. <span data-ttu-id="f0516-249">從 [驅動程式] 功能表，按一下[新增驅動程式]。</span><span class="sxs-lookup"><span data-stu-id="f0516-249">From the **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="f0516-250">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="f0516-250">Enter the following information:</span></span>

   * <span data-ttu-id="f0516-251">**名稱**：Phoenix</span><span class="sxs-lookup"><span data-stu-id="f0516-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="f0516-252">**範例 URL**：jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f0516-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="f0516-253">**類別名稱**：org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="f0516-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="f0516-254">使用者在範例 URL 中全部小寫。</span><span class="sxs-lookup"><span data-stu-id="f0516-254">User all lower case in the Example URL.</span></span> <span data-ttu-id="f0516-255">您可以使用完整 zookeeper 仲裁，以免其中一項已關閉。</span><span class="sxs-lookup"><span data-stu-id="f0516-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="f0516-256">主機名稱是 zookeeper0、zookeeper1 和 zookeeper2。</span><span class="sxs-lookup"><span data-stu-id="f0516-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL 驅動程式][img-squirrel-driver]
5. <span data-ttu-id="f0516-258">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f0516-258">Click **OK**.</span></span>

<span data-ttu-id="f0516-259">**建立 HBase 叢集的別名**</span><span class="sxs-lookup"><span data-stu-id="f0516-259">**To create an alias to the HBase cluster**</span></span>

1. <span data-ttu-id="f0516-260">從 SQuirreL，按一下左邊的 [ **別名** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f0516-260">From SQuirreL, Click the **Aliases** tab on the left.</span></span>
2. <span data-ttu-id="f0516-261">從 [別名] 功能表，按一下 [新增別名]。</span><span class="sxs-lookup"><span data-stu-id="f0516-261">From the **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="f0516-262">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="f0516-262">Enter the following information:</span></span>

   * <span data-ttu-id="f0516-263">**名稱**：HBase 叢集的名稱或您偏好的任何名稱。</span><span class="sxs-lookup"><span data-stu-id="f0516-263">**Name**: The name of the HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="f0516-264">**驅動程式**：Phoenix。</span><span class="sxs-lookup"><span data-stu-id="f0516-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="f0516-265">必須符合您在上一個程序中建立的驅動程式名稱。</span><span class="sxs-lookup"><span data-stu-id="f0516-265">This must match the driver name you created in the last procedure.</span></span>
   * <span data-ttu-id="f0516-266">**URL**：從驅動程式組態複製的 URL。</span><span class="sxs-lookup"><span data-stu-id="f0516-266">**URL**: The URL is copied from your driver configuration.</span></span> <span data-ttu-id="f0516-267">請確定使用者全部小寫。</span><span class="sxs-lookup"><span data-stu-id="f0516-267">Make sure to user all lower case.</span></span>
   * <span data-ttu-id="f0516-268">**使用者名稱**：可以是任何文字。</span><span class="sxs-lookup"><span data-stu-id="f0516-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="f0516-269">因為您在此使用 VPN 連線，所以完全不會使用使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f0516-269">Because you use VPN connectivity here, the user name is not used at all.</span></span>
   * <span data-ttu-id="f0516-270">**密碼**：可以是任何文字。</span><span class="sxs-lookup"><span data-stu-id="f0516-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL 驅動程式][img-squirrel-alias]
4. <span data-ttu-id="f0516-272">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="f0516-272">Click **Test**.</span></span>
5. <span data-ttu-id="f0516-273">按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="f0516-273">Click **Connect**.</span></span> <span data-ttu-id="f0516-274">當它建立連線時，SQuirreL 如下所示：</span><span class="sxs-lookup"><span data-stu-id="f0516-274">When it makes the connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirrel][img-squirrel]

<span data-ttu-id="f0516-276">**執行測試**</span><span class="sxs-lookup"><span data-stu-id="f0516-276">**To run a test**</span></span>

1. <span data-ttu-id="f0516-277">按一下 [物件] 索引標籤旁邊的 [SQL] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f0516-277">Click the **SQL** tab right next to the **Objects** tab.</span></span>
2. <span data-ttu-id="f0516-278">複製並貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f0516-278">Copy and paste the following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="f0516-279">按一下 [執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0516-279">Click the run button.</span></span>

    ![HBase Phoenix SQuirrel][img-squirrel-sql]
4. <span data-ttu-id="f0516-281">切換回 [ **物件** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f0516-281">Switch back to the **Objects** tab.</span></span>
5. <span data-ttu-id="f0516-282">展開別名名稱，然後再展開 **資料表**。</span><span class="sxs-lookup"><span data-stu-id="f0516-282">Expand the alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="f0516-283">您會看到底下所列的新資料表。</span><span class="sxs-lookup"><span data-stu-id="f0516-283">You shall see the new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0516-284">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0516-284">Next steps</span></span>
<span data-ttu-id="f0516-285">在本文中，您已經學會如何在 HDInsight 中使用 Apache Phoenix。</span><span class="sxs-lookup"><span data-stu-id="f0516-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="f0516-286">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f0516-286">To learn more, see</span></span>

* <span data-ttu-id="f0516-287">[HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。</span><span class="sxs-lookup"><span data-stu-id="f0516-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="f0516-288">[在 Azure 虛擬網路上佈建 HBase 叢集][hdinsight-hbase-provision-vnet]：由於 HBase 叢集已與虛擬網路整合，因此能夠部署到和應用程式相同的虛擬網路，讓應用程式得以和 HBase 直接通訊。</span><span class="sxs-lookup"><span data-stu-id="f0516-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="f0516-289">[設定 HDInsight 中的 HBase 複寫](hdinsight-hbase-replication.md)：了解如何跨兩個 Azure 資料中心設定 HBase 複寫。</span><span class="sxs-lookup"><span data-stu-id="f0516-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="f0516-290">[利用 HDInsight 中的 HBase 分析 Twitter 情感][hbase-twitter-sentiment]：了解如何使用 HDInsight 之 Hadoop 叢集中的 HBase，執行巨量資料的即時[情感分析](http://en.wikipedia.org/wiki/Sentiment_analysis)。</span><span class="sxs-lookup"><span data-stu-id="f0516-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
