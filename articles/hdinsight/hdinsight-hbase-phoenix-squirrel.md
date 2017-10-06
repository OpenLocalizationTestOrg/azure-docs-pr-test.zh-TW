---
title: "aaaUse Apache in Phoenix 和與 windows Azure HDInsight 松鼠 |Microsoft 文件"
description: "深入了解如何 toouse HDInsight 中的 Apache in Phoenix 以及 tooinstall 及設定松鼠 HDInsight 中您工作站 tooconnect tooan HBase 叢集。"
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
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="c012f-103">在 HDInsight 中搭配 Windows 型 HBase 叢集使用 Apache Phoenix 和 SQuirreL</span><span class="sxs-lookup"><span data-stu-id="c012f-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="c012f-104">深入了解如何 toouse [Apache in Phoenix](http://phoenix.apache.org/)在 HDInsight，以及如何 tooinstall 及設定松鼠 HDInsight 中您工作站 tooconnect tooan HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="c012f-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="c012f-105">如需有關 Phoenix 的詳細資訊，請參閱 [15 分鐘內了解 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)。</span><span class="sxs-lookup"><span data-stu-id="c012f-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="c012f-106">Hello in Phoenix 文法，請參閱[in Phoenix 文法](http://phoenix.apache.org/language/index.html)。</span><span class="sxs-lookup"><span data-stu-id="c012f-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="c012f-107">Hello in Phoenix HDInsight 中的版本資訊，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="c012f-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="c012f-108">hello 這個文件的唯一工作 Windows 為基礎的 HDInsight 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="c012f-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c012f-109">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="c012f-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="c012f-110">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="c012f-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c012f-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c012f-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="c012f-112">如需在 Linux 型 HDInsight 上使用 Phoenix 的相關資訊，請參閱[在 HDinsight 中搭配 Linux 型 HBase 叢集使用 Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="c012f-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="c012f-113">使用 SQLLine</span><span class="sxs-lookup"><span data-stu-id="c012f-113">Use SQLLine</span></span>
<span data-ttu-id="c012f-114">[SQLLine](http://sqlline.sourceforge.net/)是命令列公用程式 tooexecute SQL。</span><span class="sxs-lookup"><span data-stu-id="c012f-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c012f-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="c012f-115">Prerequisites</span></span>
<span data-ttu-id="c012f-116">您可以使用 SQLLine 之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="c012f-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="c012f-117">**HDInsight 中的 HBase 叢集**。</span><span class="sxs-lookup"><span data-stu-id="c012f-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="c012f-118">如需有關佈建 HBase 叢集的資訊，請參閱[開始使用 HDInsight 中的 Apache HBase][hdinsight-hbase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="c012f-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="c012f-119">**透過 hello 遠端桌面通訊協定 toohello HBase 叢集連線**。</span><span class="sxs-lookup"><span data-stu-id="c012f-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="c012f-120">如需指示，請參閱[使用 hello Azure 傳統入口網站來管理 Hadoop 叢集 HDInsight 中][hdinsight-manage-portal]。</span><span class="sxs-lookup"><span data-stu-id="c012f-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="c012f-121">**toofind 出 hello 主機名稱**</span><span class="sxs-lookup"><span data-stu-id="c012f-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="c012f-122">開啟**Hadoop 命令列**從 hello 桌面。</span><span class="sxs-lookup"><span data-stu-id="c012f-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="c012f-123">執行下列命令 tooget hello DNS 尾碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="c012f-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="c012f-124">並記下 **連線專用 DNS 尾碼**。</span><span class="sxs-lookup"><span data-stu-id="c012f-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="c012f-125">例如， *myhbasecluster.f5.internal.cloudapp.net*。</span><span class="sxs-lookup"><span data-stu-id="c012f-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="c012f-126">當您連接 tooan HBase 叢集時，您需要 tooconnect tooone 的 hello 動物園管理員使用的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="c012f-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="c012f-127">每個 HDInsight 叢集有 3 個 Zookeeper。</span><span class="sxs-lookup"><span data-stu-id="c012f-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="c012f-128">它們是 *zookeeper0*、*zookeeper1* 和 *zookeeper2*。</span><span class="sxs-lookup"><span data-stu-id="c012f-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="c012f-129">hello FQDN 會像*zookeeper2.myhbasecluster.f5.internal.cloudapp.net*。</span><span class="sxs-lookup"><span data-stu-id="c012f-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="c012f-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="c012f-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="c012f-131">開啟**Hadoop 命令列**從 hello 桌面。</span><span class="sxs-lookup"><span data-stu-id="c012f-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="c012f-132">執行下列命令 tooopen SQLLine hello:</span><span class="sxs-lookup"><span data-stu-id="c012f-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="c012f-134">hello hello 範例中所使用的命令：</span><span class="sxs-lookup"><span data-stu-id="c012f-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="c012f-135">如需詳細資訊，請參閱 [SQLLine 手冊](http://sqlline.sourceforge.net/#manual)和 [Phoenix 文法](http://phoenix.apache.org/language/index.html)。</span><span class="sxs-lookup"><span data-stu-id="c012f-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="c012f-136">使用 SQuirreL</span><span class="sxs-lookup"><span data-stu-id="c012f-136">Use SQuirreL</span></span>
<span data-ttu-id="c012f-137">[SQL 用戶端松鼠](http://squirrel-sql.sourceforge.net/)是圖形化的 Java 程式，將允許您 tooview hello JDBC 相容的資料庫結構，瀏覽 hello 資料表中的資料，發出 SQL 命令等。它可以是使用的 tooconnect tooApache in Phoenix HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="c012f-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="c012f-138">這個區段會顯示如何 tooinstall 和松鼠叢集上設定您的工作站 tooconnect tooan HBase HDInsight 中透過 VPN。</span><span class="sxs-lookup"><span data-stu-id="c012f-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c012f-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="c012f-139">Prerequisites</span></span>
<span data-ttu-id="c012f-140">Hello 程序之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="c012f-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="c012f-141">HBase 叢集部署 tooan 與 DNS 虛擬機器的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c012f-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="c012f-142">如需相關指示，請參閱[在 Azure 虛擬網路上建立 HBase 叢集][hdinsight-hbase-provision-vnet]。</span><span class="sxs-lookup"><span data-stu-id="c012f-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="c012f-143">收到 hello HBase 叢集的叢集連線特定 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="c012f-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="c012f-144">tooget 它 RDP 到 hello 叢集中，然後執行 IPConfig。</span><span class="sxs-lookup"><span data-stu-id="c012f-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="c012f-145">hello DNS 尾碼是類似於：</span><span class="sxs-lookup"><span data-stu-id="c012f-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="c012f-146">在您的工作站上下載並安裝 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="c012f-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="c012f-147">您必須從 hello 封裝 toocreate makecert 您的憑證。</span><span class="sxs-lookup"><span data-stu-id="c012f-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="c012f-148">在您的工作站上下載並安裝 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 。</span><span class="sxs-lookup"><span data-stu-id="c012f-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="c012f-149">SQuirreL SQL 用戶端 3.0 版和更新版本需要 JRE 1.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c012f-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="c012f-150">設定點對站 VPN 連線 toohello Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="c012f-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="c012f-151">設定點對站 VPN 連線包含 3 個步驟：</span><span class="sxs-lookup"><span data-stu-id="c012f-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="c012f-152">設定虛擬網路和動態路由閘道</span><span class="sxs-lookup"><span data-stu-id="c012f-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="c012f-153">建立您的憑證</span><span class="sxs-lookup"><span data-stu-id="c012f-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="c012f-154">設定 VPN 用戶端</span><span class="sxs-lookup"><span data-stu-id="c012f-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="c012f-155">請參閱[設定點對站 VPN 連線 tooan Azure 虛擬網路](../vpn-gateway/vpn-gateway-point-to-site-create.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c012f-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="c012f-156">設定虛擬網路和動態路由閘道</span><span class="sxs-lookup"><span data-stu-id="c012f-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="c012f-157">確保您已佈建 HBase 叢集的 Azure 虛擬網路中 （請參閱本章節的 hello 必要條件）。</span><span class="sxs-lookup"><span data-stu-id="c012f-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="c012f-158">hello 下一個步驟是 tooconfigure 點對站連線。</span><span class="sxs-lookup"><span data-stu-id="c012f-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="c012f-159">**tooconfigure hello 點對站連線能力**</span><span class="sxs-lookup"><span data-stu-id="c012f-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="c012f-160">登入 toohello [Azure 傳統入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="c012f-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="c012f-161">Hello 左側，按一下 **網路**。</span><span class="sxs-lookup"><span data-stu-id="c012f-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="c012f-162">按一下您所建立的 hello 虛擬網路 (請參閱[佈建 HBase 叢集的 Azure 虛擬網路上][hdinsight-hbase-provision-vnet])。</span><span class="sxs-lookup"><span data-stu-id="c012f-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="c012f-163">按一下**設定**從 hello。</span><span class="sxs-lookup"><span data-stu-id="c012f-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="c012f-164">在 hello**點對站連線能力**區段中，選取**設定點對站連線能力**。</span><span class="sxs-lookup"><span data-stu-id="c012f-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="c012f-165">設定**起始 IP**和**CIDR** toospecify hello IP 位址範圍 VPN 用戶端將從其接收 IP 位址連線時。</span><span class="sxs-lookup"><span data-stu-id="c012f-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="c012f-166">hello 範圍不能與任何 hello 範圍位於內部網路，而且 hello 您將會連接到 Azure 虛擬網路重疊。</span><span class="sxs-lookup"><span data-stu-id="c012f-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="c012f-167">例如，</span><span class="sxs-lookup"><span data-stu-id="c012f-167">For example.</span></span> <span data-ttu-id="c012f-168">如果您選取 10.0.0.0/20 hello 虛擬網路，您可以選取 10.1.0.0/24 hello 用戶端的位址空間。</span><span class="sxs-lookup"><span data-stu-id="c012f-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="c012f-169">請參閱 hello[點對站連線能力][ vnet-point-to-site-connectivity]頁面以取得詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="c012f-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="c012f-170">在 hello 虛擬網路位址空間 區段中，按一下 **加入閘道子網路**。</span><span class="sxs-lookup"><span data-stu-id="c012f-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="c012f-171">按一下**儲存**上 hello hello 頁面的底部。</span><span class="sxs-lookup"><span data-stu-id="c012f-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="c012f-172">按一下**是**tooconfirm hello 變更。</span><span class="sxs-lookup"><span data-stu-id="c012f-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="c012f-173">請等到完成 hello 系統進行變更後再繼續下一個程序 toohello hello。</span><span class="sxs-lookup"><span data-stu-id="c012f-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="c012f-174">**toocreate 動態路由閘道**</span><span class="sxs-lookup"><span data-stu-id="c012f-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="c012f-175">從 hello Azure 傳統入口網站，按一下 **儀表板**從 hello hello 頁面的頂端。</span><span class="sxs-lookup"><span data-stu-id="c012f-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="c012f-176">按一下**建立閘道**從 hello hello 頁面的底部。</span><span class="sxs-lookup"><span data-stu-id="c012f-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="c012f-177">按一下**是**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="c012f-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="c012f-178">請等到建立 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="c012f-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="c012f-179">按一下**儀表板**從 hello。</span><span class="sxs-lookup"><span data-stu-id="c012f-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="c012f-180">您會看見 hello 虛擬網路的視覺圖表：</span><span class="sxs-lookup"><span data-stu-id="c012f-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Azure 虛擬網路點對站虛擬圖表][img-vnet-diagram]

    <span data-ttu-id="c012f-182">hello 圖表會顯示 0 的用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="c012f-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="c012f-183">連接 toohello 虛擬網路之後，hello 數目將會更新的 tooone。</span><span class="sxs-lookup"><span data-stu-id="c012f-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="c012f-184">建立您的憑證</span><span class="sxs-lookup"><span data-stu-id="c012f-184">Create your certificates</span></span>
<span data-ttu-id="c012f-185">其中一種方式是使用 X.509 憑證的 toocreate hello 所隨附的憑證建立工具 (makecert.exe) [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c012f-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="c012f-186">**toocreate 自我簽署的根憑證**</span><span class="sxs-lookup"><span data-stu-id="c012f-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="c012f-187">從您的工作站，開啟命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="c012f-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="c012f-188">瀏覽 toohello Visual Studio 工具 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c012f-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="c012f-189">下列命令在 hello 面範例中的 hello 會建立與 hello 個人憑證存放區，您的工作站上安裝根憑證和也建立對應的.cer 檔案，您將於稍後上傳 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="c012f-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="c012f-190">變更您想 hello.cer 檔案 toobe HBaseVnetVPNRootCertificate 其中您要 hello 憑證 toouse hello 名稱中，位於 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="c012f-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="c012f-191">不要關閉 hello 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="c012f-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="c012f-192">您需要在 hello 下一個程序。</span><span class="sxs-lookup"><span data-stu-id="c012f-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c012f-193">因為您已建立將會產生用戶端憑證的根憑證，您可能想 tooexport 連同私密金鑰一起此憑證，並將它儲存 tooa 安全的位置，或許可以修復它。</span><span class="sxs-lookup"><span data-stu-id="c012f-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="c012f-194">**toocreate 用戶端憑證**</span><span class="sxs-lookup"><span data-stu-id="c012f-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="c012f-195">Hello 從相同的命令提示字元 (對 hello toobe hello 根憑證的建立所在的同一部電腦。</span><span class="sxs-lookup"><span data-stu-id="c012f-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="c012f-196">hello 用戶端必須產生憑證從 hello 根憑證），執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="c012f-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="c012f-197">HBaseVnetVPNRootCertificate 是 hello 根憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="c012f-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="c012f-198">它有 toomatch hello 根憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="c012f-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="c012f-199">Hello 根憑證和 hello 用戶端憑證儲存在您的個人憑證存放區，您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c012f-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="c012f-200">使用 certmgr.msc tooverify。</span><span class="sxs-lookup"><span data-stu-id="c012f-200">Use certmgr.msc tooverify.</span></span>

    ![Azure 虛擬網路點對站 VPN 憑證][img-certificate]

    <span data-ttu-id="c012f-202">用戶端憑證必須安裝在每部電腦上您想 tooconnect toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c012f-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="c012f-203">我們建議您建立唯一的用戶端憑證，每一部電腦的 tooconnect toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c012f-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="c012f-204">tooexport hello 用戶端憑證，請使用 certmgr.msc。</span><span class="sxs-lookup"><span data-stu-id="c012f-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="c012f-205">**tooupload hello 根憑證 toohello Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="c012f-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="c012f-206">從 hello Azure 傳統入口網站，按一下 **網路**hello 左側。</span><span class="sxs-lookup"><span data-stu-id="c012f-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="c012f-207">按一下 hello HBase 叢集部署到其中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c012f-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="c012f-208">按一下**憑證**從 hello。</span><span class="sxs-lookup"><span data-stu-id="c012f-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="c012f-209">按一下**上傳**hello 從下方，並指定您已建立在 hello 程序中最後一個以外的 hello 根憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="c012f-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="c012f-210">請等到 hello 憑證已匯入。</span><span class="sxs-lookup"><span data-stu-id="c012f-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="c012f-211">按一下**儀表板**hello 上方。</span><span class="sxs-lookup"><span data-stu-id="c012f-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="c012f-212">hello 虛擬圖表會顯示 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="c012f-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="c012f-213">設定 VPN 用戶端</span><span class="sxs-lookup"><span data-stu-id="c012f-213">Configure your VPN client</span></span>
<span data-ttu-id="c012f-214">**toodownload 並安裝 hello 用戶端 VPN 封裝**</span><span class="sxs-lookup"><span data-stu-id="c012f-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="c012f-215">從 hello 儀表板頁面的 hello 虛擬網路，在 hello 快速概覽區段中，按一下 **下載 hello 64 位元用戶端 VPN 封裝**或**下載 hello 32 位元用戶端 VPN 封裝**根據您工作站作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="c012f-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="c012f-216">按一下**執行**tooinstall hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="c012f-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="c012f-217">在 hello 安全性提示字元中，按一下**進一歩**，然後按一下**繼續執行**。</span><span class="sxs-lookup"><span data-stu-id="c012f-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="c012f-218">按兩下 [ **是** ]。</span><span class="sxs-lookup"><span data-stu-id="c012f-218">Click **Yes** twice.</span></span>

<span data-ttu-id="c012f-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="c012f-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="c012f-220">在您的工作站的 hello 桌面上，按一下 hello hello 工作列上的網路圖示。</span><span class="sxs-lookup"><span data-stu-id="c012f-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="c012f-221">您會看到虛擬網路名稱的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="c012f-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="c012f-222">按一下 hello VPN 連線名稱。</span><span class="sxs-lookup"><span data-stu-id="c012f-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="c012f-223">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="c012f-223">Click **Connect**.</span></span>

<span data-ttu-id="c012f-224">**tootest hello VPN 連接和網域名稱解析**</span><span class="sxs-lookup"><span data-stu-id="c012f-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="c012f-225">從 hello 工作站上，開啟 命令提示字元，且下列名稱指定 hello HBase 叢集的 DNS 尾碼的 hello 的其中一個 ping myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="c012f-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="c012f-226">安裝與設定您的工作站上的 SQuirreL</span><span class="sxs-lookup"><span data-stu-id="c012f-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="c012f-227">**tooinstall 松鼠**</span><span class="sxs-lookup"><span data-stu-id="c012f-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="c012f-228">下載 hello 松鼠 SQL 用戶端 jar 檔案從[http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation)。</span><span class="sxs-lookup"><span data-stu-id="c012f-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="c012f-229">開啟/執行 hello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="c012f-229">Open/run hello jar file.</span></span> <span data-ttu-id="c012f-230">它需要 hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html)。</span><span class="sxs-lookup"><span data-stu-id="c012f-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="c012f-231">按兩下 [ **下一步** ]。</span><span class="sxs-lookup"><span data-stu-id="c012f-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="c012f-232">指定您擁有寫入權限，並再按 hello 路徑**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c012f-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c012f-233">hello 預設安裝資料夾為 hello C:\Program Files\squirrel sql 3.6 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c012f-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="c012f-234">順序 toowrite toothis 路徑，hello 安裝程式必須授與 hello 系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="c012f-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="c012f-235">您可以開啟命令提示字元，以系統管理員身分，瀏覽 tooJava 的 bin 資料夾，然後再執行：</span><span class="sxs-lookup"><span data-stu-id="c012f-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="c012f-236">java.exe-jar [hello hello 松鼠 jar 檔案路徑]</span><span class="sxs-lookup"><span data-stu-id="c012f-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="c012f-237">按一下**確定**tooconfirm 建立 hello 目標目錄。</span><span class="sxs-lookup"><span data-stu-id="c012f-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="c012f-238">hello 預設設定是 tooinstall hello 基底和標準的封裝。</span><span class="sxs-lookup"><span data-stu-id="c012f-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="c012f-239">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c012f-239">Click **Next**.</span></span>
7. <span data-ttu-id="c012f-240">依序按兩下 [下一步] 和 [完成]。</span><span class="sxs-lookup"><span data-stu-id="c012f-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="c012f-241">**tooinstall hello in Phoenix 驅動程式**</span><span class="sxs-lookup"><span data-stu-id="c012f-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="c012f-242">hello in phoenix 驅動程式 jar 檔案位於 hello HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="c012f-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="c012f-243">hello 路徑為 hello 版本為基礎的 toohello 下列類似：</span><span class="sxs-lookup"><span data-stu-id="c012f-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="c012f-244">您需要 toocopy 它 hello [松鼠安裝資料夾] 下的 tooyour 工作站 / lib 路徑。</span><span class="sxs-lookup"><span data-stu-id="c012f-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="c012f-245">hello 最簡單方式是到 hello 叢集中，然後按一下 使用檔案複製/貼上 （CTRL + C 和 CTRL + V） toocopy tooRDP 它 tooyour 工作站。</span><span class="sxs-lookup"><span data-stu-id="c012f-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="c012f-246">**tooadd in Phoenix 驅動程式 tooSQuirreL**</span><span class="sxs-lookup"><span data-stu-id="c012f-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="c012f-247">從您的工作站開啟 SQuirreL SQL 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c012f-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="c012f-248">按一下 hello**驅動程式**hello 左邊的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c012f-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="c012f-249">從 hello**驅動程式**功能表上，按一下 **新的驅動程式**。</span><span class="sxs-lookup"><span data-stu-id="c012f-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="c012f-250">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="c012f-250">Enter hello following information:</span></span>

   * <span data-ttu-id="c012f-251">**名稱**：Phoenix</span><span class="sxs-lookup"><span data-stu-id="c012f-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="c012f-252">**範例 URL**：jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="c012f-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="c012f-253">**類別名稱**：org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="c012f-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="c012f-254">使用者在 hello 範例 URL 中的所有大小寫。</span><span class="sxs-lookup"><span data-stu-id="c012f-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="c012f-255">您可以使用完整 zookeeper 仲裁，以免其中一項已關閉。</span><span class="sxs-lookup"><span data-stu-id="c012f-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="c012f-256">hello 主機名稱為 zookeeper0、 zookeeper1 和 zookeeper2。</span><span class="sxs-lookup"><span data-stu-id="c012f-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL 驅動程式][img-squirrel-driver]
5. <span data-ttu-id="c012f-258">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c012f-258">Click **OK**.</span></span>

<span data-ttu-id="c012f-259">**toocreate 別名 toohello HBase 叢集**</span><span class="sxs-lookup"><span data-stu-id="c012f-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="c012f-260">從松鼠，按一下 hello**別名**hello 左邊的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c012f-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="c012f-261">從 hello**別名**功能表上，按一下 **新別名**。</span><span class="sxs-lookup"><span data-stu-id="c012f-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="c012f-262">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="c012f-262">Enter hello following information:</span></span>

   * <span data-ttu-id="c012f-263">**名稱**: hello 名稱 hello HBase 叢集或任何您偏好的名稱。</span><span class="sxs-lookup"><span data-stu-id="c012f-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="c012f-264">**驅動程式**：Phoenix。</span><span class="sxs-lookup"><span data-stu-id="c012f-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="c012f-265">這必須符合您在 hello 最後一個程序中建立的 hello 驅動程式名稱。</span><span class="sxs-lookup"><span data-stu-id="c012f-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="c012f-266">**URL**: hello URL 已複製從驅動程式設定。</span><span class="sxs-lookup"><span data-stu-id="c012f-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="c012f-267">請確定 toouser 所有大小寫。</span><span class="sxs-lookup"><span data-stu-id="c012f-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="c012f-268">**使用者名稱**：可以是任何文字。</span><span class="sxs-lookup"><span data-stu-id="c012f-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="c012f-269">因為您在這裡使用 VPN 連線能力，是不會在所有使用 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c012f-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="c012f-270">**密碼**：可以是任何文字。</span><span class="sxs-lookup"><span data-stu-id="c012f-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL 驅動程式][img-squirrel-alias]
4. <span data-ttu-id="c012f-272">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="c012f-272">Click **Test**.</span></span>
5. <span data-ttu-id="c012f-273">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="c012f-273">Click **Connect**.</span></span> <span data-ttu-id="c012f-274">當建立 hello 連接時，松鼠看起來像：</span><span class="sxs-lookup"><span data-stu-id="c012f-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirrel][img-squirrel]

<span data-ttu-id="c012f-276">**toorun 測試**</span><span class="sxs-lookup"><span data-stu-id="c012f-276">**toorun a test**</span></span>

1. <span data-ttu-id="c012f-277">按一下 hello **SQL**索引標籤上的權限下一步 toohello**物件** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c012f-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="c012f-278">複製並貼上下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="c012f-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="c012f-279">按一下 hello 執行 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c012f-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirrel][img-squirrel-sql]
4. <span data-ttu-id="c012f-281">切換後 toohello**物件** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c012f-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="c012f-282">展開 hello 別名名稱，然後再展開**資料表**。</span><span class="sxs-lookup"><span data-stu-id="c012f-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="c012f-283">您應該會看到 hello 底下所列的新資料表。</span><span class="sxs-lookup"><span data-stu-id="c012f-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c012f-284">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c012f-284">Next steps</span></span>
<span data-ttu-id="c012f-285">在本文中，您已經學會如何 toouse Apache in Phoenix HDInsight 中。</span><span class="sxs-lookup"><span data-stu-id="c012f-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="c012f-286">toolearn 詳細資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="c012f-286">toolearn more, see</span></span>

* <span data-ttu-id="c012f-287">[HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。</span><span class="sxs-lookup"><span data-stu-id="c012f-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="c012f-288">[佈建 Azure 虛擬網路上的 HBase 叢集][hdinsight-hbase-provision-vnet]： 與虛擬網路整合 HBase 叢集可以部署的 toohello 相同虛擬網路與您的應用程式因此應用程式可以與通訊直接 HBase。</span><span class="sxs-lookup"><span data-stu-id="c012f-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="c012f-289">[設定在 HDInsight HBase 複寫](hdinsight-hbase-replication.md)： 了解如何 tooconfigure HBase 複寫，跨兩個 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="c012f-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="c012f-290">[分析與在 HDInsight HBase Twitter 情緒][hbase-twitter-sentiment]： 了解如何 toodo 即時[情緒分析](http://en.wikipedia.org/wiki/Sentiment_analysis)的巨量資料在 HDInsight Hadoop 叢集中使用 HBase。</span><span class="sxs-lookup"><span data-stu-id="c012f-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
