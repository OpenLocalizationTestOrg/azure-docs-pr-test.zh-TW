---
title: "在 Azure HDInsight Linux 叢集上安裝 Presto | Microsoft Docs"
description: "了解如何使用指令碼動作，在以 Linux 為基礎的 HDInsight Hadoop 叢集上安裝 Presto 和 Airpal。"
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
ms.openlocfilehash: 406ef84e72d253fec51a0b37c48f326dafd511b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="94806-103">在 HDInsight Hadoop 叢集上安裝和使用 Presto</span><span class="sxs-lookup"><span data-stu-id="94806-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="94806-104">在本主題中，您會了解如何使用指令碼動作，在 HDInsight Hadoop 叢集上安裝 Presto。</span><span class="sxs-lookup"><span data-stu-id="94806-104">In this topic, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="94806-105">您也會了解如何在現有的 HDInsight 叢集上安裝 Airpal。</span><span class="sxs-lookup"><span data-stu-id="94806-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94806-106">此文件中的步驟需要使用 Linux 的 **HDInsight 3.5 Hadoop 叢集**。</span><span class="sxs-lookup"><span data-stu-id="94806-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="94806-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="94806-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="94806-108">如需詳細資訊，請參閱 [HDInsight 版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="94806-109">什麼是 Presto？</span><span class="sxs-lookup"><span data-stu-id="94806-109">What is Presto?</span></span>
<span data-ttu-id="94806-110">[Presto](https://prestodb.io/overview.html) 是巨量資料的快速分散式 SQL 查詢引擎。</span><span class="sxs-lookup"><span data-stu-id="94806-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="94806-111">Presto 適合數 PB 資料的互動式查詢。</span><span class="sxs-lookup"><span data-stu-id="94806-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="94806-112">如需 Presto 的元件以及它們共同運作方式的詳細資訊，請參閱 [Presto 概念](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst)。</span><span class="sxs-lookup"><span data-stu-id="94806-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="94806-113">透過 HDInsight 叢集提供的元件會受到完整支援，且 Microsoft 支援服務將協助釐清與解決這些元件的相關問題。</span><span class="sxs-lookup"><span data-stu-id="94806-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="94806-114">自訂元件 (例如 Presto) 會獲得商務上合理的支援，協助您進一步針對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="94806-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="94806-115">如此可能會進而解決問題，或要求您利用可用管道，以找出開放原始碼技術，從中了解該技術的深度專業知識。</span><span class="sxs-lookup"><span data-stu-id="94806-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="94806-116">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="94806-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="94806-117">另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="94806-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="94806-118">使用指令碼動作來安裝 Presto</span><span class="sxs-lookup"><span data-stu-id="94806-118">Install Presto using script action</span></span>

<span data-ttu-id="94806-119">本節提供如何在使用 Azure 入口網站建立新叢集時使用範例指令碼的指示。</span><span class="sxs-lookup"><span data-stu-id="94806-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="94806-120">使用[佈建以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)中的步驟，開始佈建叢集。</span><span class="sxs-lookup"><span data-stu-id="94806-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="94806-121">請確定您是使用**自訂**叢集建立流程來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="94806-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="94806-122">請務必確定您所建立的叢集符合下列需求。</span><span class="sxs-lookup"><span data-stu-id="94806-122">You must ensure that the cluster you create meets the following requirements.</span></span>

    <span data-ttu-id="94806-123">a.</span><span class="sxs-lookup"><span data-stu-id="94806-123">a.</span></span> <span data-ttu-id="94806-124">必須為隨附 HDInsight 3.5 版的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="94806-124">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="94806-125">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="94806-125">b.</span></span> <span data-ttu-id="94806-126">它必須使用 Azure 儲存體作為資料存放區。</span><span class="sxs-lookup"><span data-stu-id="94806-126">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="94806-127">尚未支援在將 Azure Data Lake Store 作為儲存體選項的叢集上使用 Presto。</span><span class="sxs-lookup"><span data-stu-id="94806-127">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![使用自訂選項建立 HDInsight 叢集](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="94806-129">在 [進階設定] 刀鋒視窗中，選取 [指令碼動作]，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="94806-129">On the **Advanced settings** blade, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="94806-130">**名稱**：輸入指令碼動作的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="94806-130">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="94806-131">**Bash 指令碼 URI**：`https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="94806-131">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="94806-132">**HEAD**：勾選此選項</span><span class="sxs-lookup"><span data-stu-id="94806-132">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="94806-133">**WORKER**：勾選此選項</span><span class="sxs-lookup"><span data-stu-id="94806-133">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="94806-134">**ZOOKEEPER**︰清除此核取方塊</span><span class="sxs-lookup"><span data-stu-id="94806-134">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="94806-135">**參數**：將此欄位保留空白</span><span class="sxs-lookup"><span data-stu-id="94806-135">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="94806-136">在 [指令碼動作] 刀鋒視窗的底部，按一下 [選取] 按鈕來儲存設定。</span><span class="sxs-lookup"><span data-stu-id="94806-136">At the bottom of the **Script Actions** blade, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="94806-137">最後，按一下 [進階設定] 刀鋒視窗底部的 [選取] 按鈕來儲存設定資訊。</span><span class="sxs-lookup"><span data-stu-id="94806-137">Finally, click  the **Select** button at the bottom of the **Advanced Settings** blade to save the configuration information.</span></span>

4. <span data-ttu-id="94806-138">繼續如 [佈建以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)中所述佈建叢集。</span><span class="sxs-lookup"><span data-stu-id="94806-138">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="94806-139">Azure PowerShell、Azure CLI、HDInsight .NET SDK 或 Azure Resource Manager 範本也可用來套用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="94806-139">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="94806-140">您也可以將指令碼動作套用到執行中的叢集上。</span><span class="sxs-lookup"><span data-stu-id="94806-140">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="94806-141">如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-141">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="94806-142">使用 Presto 搭配 HDInsight</span><span class="sxs-lookup"><span data-stu-id="94806-142">Use Presto with HDInsight</span></span>

<span data-ttu-id="94806-143">在使用上述步驟將 Presto 安裝後，請執行下列步驟來使用 HDInsight 叢集中的 Presto。</span><span class="sxs-lookup"><span data-stu-id="94806-143">Perform the following steps to use Presto in an HDInsight cluster after you have installed it using the steps described above.</span></span>

1. <span data-ttu-id="94806-144">使用 SSH 連線到 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="94806-144">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="94806-145">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="94806-146">使用下列命令啟動 Presto 殼層。</span><span class="sxs-lookup"><span data-stu-id="94806-146">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="94806-147">在所有 HDInsight 叢集中預設可用的範例資料表 (**hivesampletable**) 上執行查詢。</span><span class="sxs-lookup"><span data-stu-id="94806-147">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="94806-148">依預設，已設定 Presto 的 [Hive](https://prestodb.io/docs/current/connector/hive.html) 和 [TPCH](https://prestodb.io/docs/current/connector/tpch.html) 連接器。</span><span class="sxs-lookup"><span data-stu-id="94806-148">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="94806-149">Hive 連接器會設定為使用預設已安裝的 Hive 安裝，以便 Hive 的所有資料表都會自動顯示在 Presto 中。</span><span class="sxs-lookup"><span data-stu-id="94806-149">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="94806-150">如需 Presto 使用方式的詳細說明，請參閱 [Presto 文件](https://prestodb.io/docs/current/index.html)。</span><span class="sxs-lookup"><span data-stu-id="94806-150">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="94806-151">使用 Airpal 搭配 Presto</span><span class="sxs-lookup"><span data-stu-id="94806-151">Use Airpal with Presto</span></span>

<span data-ttu-id="94806-152">[Airpal](https://github.com/airbnb/airpal#airpal) 是 Presto 以 web 作為基礎的開放原始碼查詢介面。</span><span class="sxs-lookup"><span data-stu-id="94806-152">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="94806-153">如需有關 Airpal 的詳細資訊，請參閱 [Airpal 文件](https://github.com/airbnb/airpal#airpal)。</span><span class="sxs-lookup"><span data-stu-id="94806-153">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="94806-154">在本節中，我們討論已安裝 Presto 的 HDInsight Hadoop 叢集**在 edgenode 上安裝 Airpal** 的步驟。</span><span class="sxs-lookup"><span data-stu-id="94806-154">In this section, we look at the steps to **install Airpal on the edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="94806-155">這將確保可透過網際網路使用 Airpal web 查詢介面。</span><span class="sxs-lookup"><span data-stu-id="94806-155">This ensures that the Airpal web query interface is available over the Internet.</span></span>

1. <span data-ttu-id="94806-156">使用 SSH 連線到已安裝 Presto 的 HDInsight 叢集前端節點︰</span><span class="sxs-lookup"><span data-stu-id="94806-156">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="94806-157">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-157">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="94806-158">一旦連線後，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="94806-158">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="94806-159">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="94806-159">You should see an output like the following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="94806-160">記下輸出中的 **value** 屬性值。</span><span class="sxs-lookup"><span data-stu-id="94806-160">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="94806-161">您在叢集 edgenode 上安裝 Airpal 時將會需要這個值。</span><span class="sxs-lookup"><span data-stu-id="94806-161">You will need this while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="94806-162">上述輸出中，您所需要的值是 **10.0.0.12:9090**。</span><span class="sxs-lookup"><span data-stu-id="94806-162">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="94806-163">使用**[這裡](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**的範本來建立 HDInsight 叢集 edgenode 並提供值，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="94806-163">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![HDInsight 在 Presto 叢集上安裝 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="94806-165">按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="94806-165">Click **Purchase**.</span></span>

6. <span data-ttu-id="94806-166">將變更套用到叢集設定後，您可以使用下列步驟來存取 Airpal web 介面。</span><span class="sxs-lookup"><span data-stu-id="94806-166">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    <span data-ttu-id="94806-167">a.</span><span class="sxs-lookup"><span data-stu-id="94806-167">a.</span></span> <span data-ttu-id="94806-168">從叢集刀鋒視窗中，按一下 [應用程式]。</span><span class="sxs-lookup"><span data-stu-id="94806-168">From the cluster blade, click **Applications**.</span></span>

    ![HDInsight 在 Presto 叢集上啟動 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="94806-170">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="94806-170">b.</span></span> <span data-ttu-id="94806-171">從 [安裝應用程式] 刀鋒視窗中，針對 airpal 按一下 [入口網站]。</span><span class="sxs-lookup"><span data-stu-id="94806-171">From the **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![HDInsight 在 Presto 叢集上啟動 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="94806-173">c.</span><span class="sxs-lookup"><span data-stu-id="94806-173">c.</span></span> <span data-ttu-id="94806-174">出現提示時，輸入您在建立 HDInsight Hadoop 叢集時指定的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="94806-174">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="94806-175">在 HDInsight 叢集上自訂 Presto 安裝</span><span class="sxs-lookup"><span data-stu-id="94806-175">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="94806-176">在 HDInsight Hadoop 叢集上安裝 Presto 之後，您可以自訂安裝來進行變更，例如更新記憶體設定、變更連接器等。請執行下列步驟來進行此作業。</span><span class="sxs-lookup"><span data-stu-id="94806-176">After you have installed Presto on an HDInsight Hadoop cluster, you can customize the installation to make changes such as update memory settings, change connectors, etc. Perform the following steps to do so.</span></span>

1. <span data-ttu-id="94806-177">使用 SSH 連線到已安裝 Presto 的 HDInsight 叢集前端節點︰</span><span class="sxs-lookup"><span data-stu-id="94806-177">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="94806-178">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-178">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="94806-179">在 `/var/lib/presto/presto-hdinsight-master/appConfig-default.json` 檔案中進行設定變更。</span><span class="sxs-lookup"><span data-stu-id="94806-179">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="94806-180">如需 Presto 設定的詳細資訊，請參閱[以 YARN 作為基礎之叢集的 Presto 設定](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html)。</span><span class="sxs-lookup"><span data-stu-id="94806-180">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="94806-181">將 Presto 目前執行中的執行個體終止並刪除。</span><span class="sxs-lookup"><span data-stu-id="94806-181">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="94806-182">使用自訂來啟動 Presto 的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="94806-182">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="94806-183">等候新的執行個體就緒，並記下 Presto 協調者地址。</span><span class="sxs-lookup"><span data-stu-id="94806-183">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="94806-184">產生執行 Presto 之 HDInsight 叢集的基準測試資料</span><span class="sxs-lookup"><span data-stu-id="94806-184">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="94806-185">TPC-DS 是業界標準，可用於測量許多決策支援系統 (包括巨量資料系統) 的效能。</span><span class="sxs-lookup"><span data-stu-id="94806-185">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="94806-186">您可以在 HDInsight 叢集上使用 Presto 來產生資料，並將它與您自己的 HDInsight 基準測試資料比較，從而進行評估。</span><span class="sxs-lookup"><span data-stu-id="94806-186">You can use Presto on HDInsight clusters to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="94806-187">如需詳細資訊，請參閱[這裡](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-187">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="94806-188">另請參閱</span><span class="sxs-lookup"><span data-stu-id="94806-188">See also</span></span>
* <span data-ttu-id="94806-189">[在 HDInsight 叢集上安裝及使用 Hue](hdinsight-hadoop-hue-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-189">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="94806-190">Hue 是 Web UI，可讓您更輕鬆地建立、執行及儲存 Pig 和 Hive 工作，以及瀏覽您的 HDInsight 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="94806-190">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="94806-191">[在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-191">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="94806-192">在 HDInsight Hadoop 叢集上使用叢集自訂安裝 Giraph。</span><span class="sxs-lookup"><span data-stu-id="94806-192">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="94806-193">Giraph 可讓您利用 Hadoop 執行圖形處理，且可以搭配 Azure HDInsight 一起使用。</span><span class="sxs-lookup"><span data-stu-id="94806-193">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="94806-194">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="94806-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="94806-195">在 HDInsight Hadoop 叢集上使用叢集自訂安裝 Solr。</span><span class="sxs-lookup"><span data-stu-id="94806-195">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="94806-196">Solr 可讓您對儲存的資料執行功能強大的搜尋作業。</span><span class="sxs-lookup"><span data-stu-id="94806-196">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
