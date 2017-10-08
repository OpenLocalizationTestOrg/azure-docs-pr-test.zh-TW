---
title: "aaaInstall 照片 on Azure HDInsight Linux 叢集 |Microsoft 文件"
description: "了解如何 tooinstall 照片和 Airpal 上以 Linux 為基礎的 HDInsight Hadoop 叢集使用指令碼動作。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="42f31-103">在 HDInsight Hadoop 叢集上安裝和使用 Presto</span><span class="sxs-lookup"><span data-stu-id="42f31-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="42f31-104">在本主題中，您學會如何 tooinstall 照片上 HDInsight Hadoop 叢集使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="42f31-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="42f31-105">您也學到如何 tooinstall Airpal 對現有的 Presto HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="42f31-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42f31-106">hello 本文件中的步驟需要**HDInsight 3.5 Hadoop 叢集**使用 Linux。</span><span class="sxs-lookup"><span data-stu-id="42f31-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="42f31-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="42f31-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="42f31-108">如需詳細資訊，請參閱 [HDInsight 版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="42f31-109">什麼是 Presto？</span><span class="sxs-lookup"><span data-stu-id="42f31-109">What is Presto?</span></span>
<span data-ttu-id="42f31-110">[Presto](https://prestodb.io/overview.html) 是巨量資料的快速分散式 SQL 查詢引擎。</span><span class="sxs-lookup"><span data-stu-id="42f31-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="42f31-111">Presto 適合數 PB 資料的互動式查詢。</span><span class="sxs-lookup"><span data-stu-id="42f31-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="42f31-112">照片和它們如何共同運作的 hello 元件詳細資訊，請參閱[馬上概念](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst)。</span><span class="sxs-lookup"><span data-stu-id="42f31-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="42f31-113">完全支援隨附 hello HDInsight 叢集的元件，而且 Microsoft 支援服務將會說明 tooisolate 及解決問題的相關的 toothese 元件。</span><span class="sxs-lookup"><span data-stu-id="42f31-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="42f31-114">自訂元件，例如照片，會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="42f31-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="42f31-115">這可能會導致解決 hello 問題，或詢問您 tooengage hello 可用的頻道開啟原始碼技術找到深層的專業知識，針對該項技術。</span><span class="sxs-lookup"><span data-stu-id="42f31-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="42f31-116">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="42f31-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="42f31-117">使用指令碼動作來安裝 Presto</span><span class="sxs-lookup"><span data-stu-id="42f31-117">Install Presto using script action</span></span>

<span data-ttu-id="42f31-118">本節提供如何 toouse hello 範例指令碼時建立新叢集使用 hello Azure 入口網站的指示。</span><span class="sxs-lookup"><span data-stu-id="42f31-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="42f31-119">開始使用中的 hello 步驟佈建叢集[佈建 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="42f31-120">請確定您建立使用 hello hello 叢集**自訂**叢集建立流程。</span><span class="sxs-lookup"><span data-stu-id="42f31-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="42f31-121">您必須確定您建立該 hello 叢集符合下列需求的 hello。</span><span class="sxs-lookup"><span data-stu-id="42f31-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="42f31-122">a.</span><span class="sxs-lookup"><span data-stu-id="42f31-122">a.</span></span> <span data-ttu-id="42f31-123">必須為隨附 HDInsight 3.5 版的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="42f31-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="42f31-124">b.</span><span class="sxs-lookup"><span data-stu-id="42f31-124">b.</span></span> <span data-ttu-id="42f31-125">它必須使用 Azure 儲存體與 hello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="42f31-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="42f31-126">尚未支援使用 Presto 做 hello 儲存選項使用 Azure Data Lake Store 的叢集上。</span><span class="sxs-lookup"><span data-stu-id="42f31-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![使用自訂選項建立 HDInsight 叢集](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="42f31-128">在 hello**進階設定**刀鋒視窗中，選取**指令碼動作**，並提供下列 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="42f31-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="42f31-129">**名稱**： 輸入 hello 指令碼動作的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="42f31-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="42f31-130">**Bash 指令碼 URI**：`https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="42f31-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="42f31-131">**HEAD**：勾選此選項</span><span class="sxs-lookup"><span data-stu-id="42f31-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="42f31-132">**WORKER**：勾選此選項</span><span class="sxs-lookup"><span data-stu-id="42f31-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="42f31-133">**ZOOKEEPER**︰清除此核取方塊</span><span class="sxs-lookup"><span data-stu-id="42f31-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="42f31-134">**參數**：將此欄位保留空白</span><span class="sxs-lookup"><span data-stu-id="42f31-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="42f31-135">在 hello 底部 hello**指令碼動作**刀鋒視窗中，按一下 hello**選取**按鈕 toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="42f31-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="42f31-136">最後，按一下 hello**選取**在 hello hello 底部的按鈕**進階設定**刀鋒視窗 toosave hello 組態資訊。</span><span class="sxs-lookup"><span data-stu-id="42f31-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="42f31-137">繼續中所述，佈建 hello 叢集[佈建 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="42f31-138">Azure PowerShell、 hello Azure CLI、 hello HDInsight.NET SDK 或 Azure 資源管理員範本也可以使用的 tooapply 指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="42f31-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="42f31-139">您也可以套用指令碼動作 tooalready 執行中的叢集。</span><span class="sxs-lookup"><span data-stu-id="42f31-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="42f31-140">如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="42f31-141">使用 Presto 搭配 HDInsight</span><span class="sxs-lookup"><span data-stu-id="42f31-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="42f31-142">執行之後，您必須安裝它使用 hello 上面所述的步驟，請遵循步驟 toouse 照片 HDInsight 叢集中的 hello。</span><span class="sxs-lookup"><span data-stu-id="42f31-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="42f31-143">連線使用 SSH toohello HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="42f31-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="42f31-144">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="42f31-145">啟動 hello 馬上 shell 會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="42f31-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="42f31-146">在所有 HDInsight 叢集中預設可用的範例資料表 (**hivesampletable**) 上執行查詢。</span><span class="sxs-lookup"><span data-stu-id="42f31-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="42f31-147">依預設，已設定 Presto 的 [Hive](https://prestodb.io/docs/current/connector/hive.html) 和 [TPCH](https://prestodb.io/docs/current/connector/tpch.html) 連接器。</span><span class="sxs-lookup"><span data-stu-id="42f31-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="42f31-148">Hive 連接器是設定的 toouse hello 預設安裝 Hive 安裝，因此登錄區中的所有 hello 資料表都會自動顯示在照片。</span><span class="sxs-lookup"><span data-stu-id="42f31-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="42f31-149">如需 Presto 使用方式的詳細說明，請參閱 [Presto 文件](https://prestodb.io/docs/current/index.html)。</span><span class="sxs-lookup"><span data-stu-id="42f31-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="42f31-150">使用 Airpal 搭配 Presto</span><span class="sxs-lookup"><span data-stu-id="42f31-150">Use Airpal with Presto</span></span>

<span data-ttu-id="42f31-151">[Airpal](https://github.com/airbnb/airpal#airpal) 是 Presto 以 web 作為基礎的開放原始碼查詢介面。</span><span class="sxs-lookup"><span data-stu-id="42f31-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="42f31-152">如需有關 Airpal 的詳細資訊，請參閱 [Airpal 文件](https://github.com/airbnb/airpal#airpal)。</span><span class="sxs-lookup"><span data-stu-id="42f31-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="42f31-153">在本節中，我們查看 hello 步驟太**hello edgenode 上安裝 Airpal** HDInsight Hadoop 叢集中已有照片安裝。</span><span class="sxs-lookup"><span data-stu-id="42f31-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="42f31-154">這可確保該 hello Airpal web 查詢介面是透過網際網路 hello。</span><span class="sxs-lookup"><span data-stu-id="42f31-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="42f31-155">使用 SSH，連線 toohello 的 hello Presto 已安裝的 HDInsight 叢集的前端節點：</span><span class="sxs-lookup"><span data-stu-id="42f31-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="42f31-156">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="42f31-157">一旦連線後，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="42f31-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="42f31-158">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="42f31-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="42f31-159">從 hello 輸出，請注意 hello hello 值**值**屬性。</span><span class="sxs-lookup"><span data-stu-id="42f31-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="42f31-160">您將需要此安裝 Airpal hello 叢集 edgenode 上時。</span><span class="sxs-lookup"><span data-stu-id="42f31-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="42f31-161">從 hello 上述輸出中，您將需要的 hello 值是**10.0.0.12:9090**。</span><span class="sxs-lookup"><span data-stu-id="42f31-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="42f31-162">使用 hello 範本**[這裡](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate 在 HDInsight 叢集 edgenode 並提供 hello 值 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="42f31-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![HDInsight 在 Presto 叢集上安裝 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="42f31-164">按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="42f31-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="42f31-165">Hello 變更套用的 toohello 叢集設定後，您可以使用下列步驟的 hello 存取 hello Airpal web 介面。</span><span class="sxs-lookup"><span data-stu-id="42f31-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="42f31-166">a.</span><span class="sxs-lookup"><span data-stu-id="42f31-166">a.</span></span> <span data-ttu-id="42f31-167">從 hello 叢集刀鋒視窗中，按一下 **應用程式**。</span><span class="sxs-lookup"><span data-stu-id="42f31-167">From hello cluster blade, click **Applications**.</span></span>

    ![HDInsight 在 Presto 叢集上啟動 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="42f31-169">b.</span><span class="sxs-lookup"><span data-stu-id="42f31-169">b.</span></span> <span data-ttu-id="42f31-170">從 hello**安裝應用程式**刀鋒視窗中，按一下 **入口網站**針對 airpal。</span><span class="sxs-lookup"><span data-stu-id="42f31-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![HDInsight 在 Presto 叢集上啟動 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="42f31-172">c.</span><span class="sxs-lookup"><span data-stu-id="42f31-172">c.</span></span> <span data-ttu-id="42f31-173">出現提示時，輸入 hello 建立 hello HDInsight Hadoop 叢集時，您指定的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="42f31-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="42f31-174">在 HDInsight 叢集上自訂 Presto 安裝</span><span class="sxs-lookup"><span data-stu-id="42f31-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="42f31-175">HDInsight Hadoop 叢集上安裝多照片之後，您可以自訂 hello 安裝 toomake 變更，例如更新記憶體設定、 變更連接器等。執行下列步驟 toodo 因此 hello。</span><span class="sxs-lookup"><span data-stu-id="42f31-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="42f31-176">使用 SSH，連線 toohello 的 hello Presto 已安裝的 HDInsight 叢集的前端節點：</span><span class="sxs-lookup"><span data-stu-id="42f31-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="42f31-177">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="42f31-178">在 hello 檔案進行組態變更`/var/lib/presto/presto-hdinsight-master/appConfig-default.json`。</span><span class="sxs-lookup"><span data-stu-id="42f31-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="42f31-179">如需 Presto 設定的詳細資訊，請參閱[以 YARN 作為基礎之叢集的 Presto 設定](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html)。</span><span class="sxs-lookup"><span data-stu-id="42f31-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="42f31-180">停止和終止 hello 目前的執行個體照片。</span><span class="sxs-lookup"><span data-stu-id="42f31-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="42f31-181">啟動與 hello 自訂的照片的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="42f31-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="42f31-182">等候 hello 新執行個體 toobe 就緒，並記下馬上協調器位址。</span><span class="sxs-lookup"><span data-stu-id="42f31-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="42f31-183">產生執行 Presto 之 HDInsight 叢集的基準測試資料</span><span class="sxs-lookup"><span data-stu-id="42f31-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="42f31-184">TPC DS 是 hello 業界標準的測量 hello 的許多決策支援系統，包括巨量資料系統的效能。</span><span class="sxs-lookup"><span data-stu-id="42f31-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="42f31-185">您可以使用 Presto HDInsight 叢集 toogenerate 資料，並評估它與您的 HDInsight 基準資料會比較方式。</span><span class="sxs-lookup"><span data-stu-id="42f31-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="42f31-186">如需詳細資訊，請參閱[這裡](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="42f31-187">另請參閱</span><span class="sxs-lookup"><span data-stu-id="42f31-187">See also</span></span>
* <span data-ttu-id="42f31-188">[在 HDInsight 叢集上安裝及使用 Hue](hdinsight-hadoop-hue-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="42f31-189">色調是 web UI，讓您輕鬆 toocreate，執行並儲存 Pig 和 Hive 工作，以及做為瀏覽 hello HDInsight 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="42f31-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="42f31-190">[在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="42f31-191">使用叢集自訂 tooinstall Giraph 上 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="42f31-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="42f31-192">Giraph 可讓您使用 Hadoop，處理 tooperform 圖形，並可以搭配 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="42f31-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="42f31-193">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="42f31-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="42f31-194">使用叢集自訂 tooinstall Solr 上 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="42f31-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="42f31-195">Solr 可讓您儲存的資料 tooperform 功能強大的搜尋作業。</span><span class="sxs-lookup"><span data-stu-id="42f31-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
