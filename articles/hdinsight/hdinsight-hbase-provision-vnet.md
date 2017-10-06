---
title: "在虛擬網路-Azure 中的 aaaCreate HBase 叢集 |Microsoft 文件"
description: "開始在 Azure HDInsight 中使用 HBase。 了解 Azure 虛擬網路上 toocreate HDInsight HBase 叢集的方式。"
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="5b5f9-104">在 Azure 虛擬網路的 HDInsight 上建立 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="5b5f9-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="5b5f9-105">了解如何 toocreate Azure HDInsight HBase 叢集[Azure 虛擬網路][1]。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="5b5f9-106">與虛擬網路整合 HBase 叢集可以部署的 toohello 相同虛擬網路與您的應用程式因此應用程式可直接通訊使用 HBase。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="5b5f9-107">hello 優點包括：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-107">hello benefits include:</span></span>

* <span data-ttu-id="5b5f9-108">直接連線的 hello web 應用程式 toohello hello HBase 叢集節點，可讓通訊透過 HBase Java 遠端程序呼叫 (RPC) Api。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="5b5f9-109">透過使流量不須經過多個閘道器及負載平衡器，以提升其效能。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="5b5f9-110">hello 能力 tooprocess 機密資訊以更安全的方式，而不會讓公用端點。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5b5f9-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="5b5f9-111">Prerequisites</span></span>
<span data-ttu-id="5b5f9-112">開始本教學課程之前，您必須具備下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5b5f9-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="5b5f9-113">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-113">**An Azure subscription**.</span></span> <span data-ttu-id="5b5f9-114">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5b5f9-115">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="5b5f9-116">請參閱 [安裝及使用 Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="5b5f9-117">在虛擬網路上建立 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="5b5f9-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="5b5f9-118">在本節中，您必須建立以 Linux 為基礎的 HBase 叢集與 hello 相依 Azure 儲存體帳戶中的 Azure 虛擬網路使用[Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="5b5f9-119">適用於其他叢集建立方法，並了解 hello 設定，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="5b5f9-120">如需有關使用範本 toocreate Hadoop 叢集 HDInsight 中，請參閱 <<c0> [ 建立 Hadoop 叢集 HDInsight 使用 Azure Resource Manager 範本中](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="5b5f9-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="5b5f9-121">有些屬性是硬式編碼成 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="5b5f9-122">例如：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-122">For example:</span></span>
>
> * <span data-ttu-id="5b5f9-123">**位置**：美國東部 2</span><span class="sxs-lookup"><span data-stu-id="5b5f9-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="5b5f9-124">**叢集版本**：3.5</span><span class="sxs-lookup"><span data-stu-id="5b5f9-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="5b5f9-125">**叢集背景工作節點計數**：2</span><span class="sxs-lookup"><span data-stu-id="5b5f9-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="5b5f9-126">**預設儲存體帳戶**：唯一的字串</span><span class="sxs-lookup"><span data-stu-id="5b5f9-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="5b5f9-127">**虛擬網路名稱**：&lt;叢集名稱>-vnet</span><span class="sxs-lookup"><span data-stu-id="5b5f9-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="5b5f9-128">**虛擬網路位址空間**10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5b5f9-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="5b5f9-129">**子網路名稱**：subnet1</span><span class="sxs-lookup"><span data-stu-id="5b5f9-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="5b5f9-130">**子網路位址範圍**：10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5b5f9-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="5b5f9-131">&lt;叢集名稱 > 取代為您提供使用 hello 範本時的 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="5b5f9-132">按一下下列映像 tooopen hello 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="5b5f9-133">hello 範本位於[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="5b5f9-134">從 hello**自訂部署**刀鋒視窗中，輸入下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b5f9-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="5b5f9-135">**訂用帳戶**： 選取 使用的 Azure 訂用帳戶 toocreate hello HDInsight 叢集，hello 相依的儲存體帳戶，hello Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="5b5f9-136">**資源群組**：選取 [新建] 並指定新的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="5b5f9-137">**位置**： 選取 hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="5b5f9-138">**ClusterName**： 輸入建立 hello Hadoop 叢集 toobe 的名稱。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="5b5f9-139">**叢集登入名稱和密碼**: hello 預設登入名稱是**admin**。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="5b5f9-140">**SSH 使用者名稱和密碼**: hello 預設使用者名稱是**sshuser**。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="5b5f9-141">您可以將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-141">You can rename it.</span></span>
   * <span data-ttu-id="5b5f9-142">**我同意 toohello 使用條款 hello 上述**: （選取）</span><span class="sxs-lookup"><span data-stu-id="5b5f9-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="5b5f9-143">按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-143">Click **Purchase**.</span></span> <span data-ttu-id="5b5f9-144">大約需要約 20 分鐘 toocreate 叢集。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="5b5f9-145">一旦建立 hello 叢集後，您可以按一下 hello 叢集刀鋒視窗中 hello 入口 tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="5b5f9-146">完成 hello 教學課程之後，您可能想 toodelete hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="5b5f9-147">利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="5b5f9-148">您也需支付 HDInsight 叢集的費用 (即使未使用)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="5b5f9-149">由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="5b5f9-150">刪除叢集的 hello 指示，請參閱[HDInsight 中使用的管理 Hadoop 叢集 hello Azure 入口網站](hdinsight-administer-use-management-portal.md#delete-clusters)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="5b5f9-151">toobegin 使用新的 HBase 叢集，您可以使用 hello 程序中找到[開始透過 HDInsight 中的 Hadoop 使用 HBase](hdinsight-hbase-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="5b5f9-152">連接使用 HBase Java RPC Api toohello HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="5b5f9-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="5b5f9-153">建立作為服務 (IaaS) 至虛擬機器的基礎結構 hello 相同 Azure 虛擬網路和 hello 相同子網路。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="5b5f9-154">如需建立新的 IaaS 虛擬機器的指示，請參閱[建立執行 Windows Server 的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="5b5f9-155">當遵循本文件中的 hello 步驟，您必須使用 hello hello 網路設定的值：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="5b5f9-156">**虛擬網路**：&lt;叢集名稱>-vnet</span><span class="sxs-lookup"><span data-stu-id="5b5f9-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="5b5f9-157">**子網路**：subnet1</span><span class="sxs-lookup"><span data-stu-id="5b5f9-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5b5f9-158">取代&lt;叢集名稱 > hello 名稱時所使用在先前步驟中建立 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="5b5f9-159">使用這些值，hello 虛擬機器會放置在 hello 相同虛擬網路和子網路與 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="5b5f9-160">此設定可讓它們 toodirectly 與對方進行通訊。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="5b5f9-161">沒有方法 toocreate 與空白邊緣節點的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="5b5f9-162">hello 邊緣節點可以是使用的 toomanage hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="5b5f9-163">如需詳細資訊，請參閱 [Use empty edge nodes in HDInsight (在 HDInsight 中使用空白的邊緣節點)](hdinsight-apps-use-edge-node.md)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="5b5f9-164">當從遠端使用 Java 應用程式 tooconnect tooHBase，您必須使用 hello 完整的網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="5b5f9-165">toodetermine，您必須取得 hello HBase 叢集 hello 連線特定 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="5b5f9-166">toodo，您可以使用其中一個 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="5b5f9-167">使用 Web 瀏覽器 toomake Ambari 呼叫：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="5b5f9-168">瀏覽 toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / 裝載？ minimal_response = true。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="5b5f9-169">它會以 hello DNS 後置字元的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="5b5f9-170">使用 hello Ambari 網站：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="5b5f9-171">瀏覽過 https://&lt;ClusterName >。.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="5b5f9-172">按一下**主機**從 hello 上方的功能表。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="5b5f9-173">使用 Curl toomake REST 呼叫：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="5b5f9-174">在 hello JavaScript Object Notation (JSON) 傳回的資料，尋找 hello"host_name"項目。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="5b5f9-175">它包含 hello FQDN hello hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="5b5f9-176">例如：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="5b5f9-177">hello 部分 hello 網域名稱 hello 叢集名稱開頭是 hello DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="5b5f9-178">例如，mycluster.b1.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="5b5f9-179">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b5f9-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="5b5f9-180">使用下列 Azure PowerShell 指令碼 tooregister hello 的 hello **Get ClusterDetail**函式，它可以是使用的 tooreturn hello DNS 尾碼：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="5b5f9-181">執行 hello Azure PowerShell 指令碼之後, 使用 hello 下列命令的 tooreturn hello DNS 尾碼來使用 hello **Get ClusterDetail**函式。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="5b5f9-182">使用此命令時，請指定您的 HDInsight HBase 叢集名稱、管理員名稱和管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="5b5f9-183">此命令會傳回 hello DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="5b5f9-184">例如， **yourclustername.b4.internal.cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="5b5f9-185">hello 虛擬機器的 tooverify 可以與 hello HBase 叢集，請使用 hello 命令`ping headnode0.<dns suffix>`從 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="5b5f9-186">例如，ping headnode0.mycluster.b1.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="5b5f9-187">toouse 這項資訊在 Java 應用程式中，您可以依照中的 hello 步驟[使用 Maven toobuild Java 應用程式與 HDInsight (Hadoop) 使用 HBase](hdinsight-hbase-build-java-maven.md) toocreate 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="5b5f9-188">toohave hello 應用程式連接 tooa 遠端 HBase 伺服器，修改 hello **hbase-site.xml**中的檔案，此範例 toouse hello FQDN 動物園管理員。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="5b5f9-189">例如：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="5b5f9-190">如需有關名稱解析在 Azure 虛擬網路中，包括如何 toouse DNS 伺服器，請參閱[名稱解析 (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5b5f9-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b5f9-191">Next steps</span></span>
<span data-ttu-id="5b5f9-192">在本教學課程中，您學到如何 toocreate HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="5b5f9-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="5b5f9-193">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5b5f9-193">toolearn more, see:</span></span>

* [<span data-ttu-id="5b5f9-194">開始使用 HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b5f9-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="5b5f9-195">在 HDInsight 中使用空白邊緣節點</span><span class="sxs-lookup"><span data-stu-id="5b5f9-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="5b5f9-196">在 HDInsight 中設定 HBase 複寫</span><span class="sxs-lookup"><span data-stu-id="5b5f9-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="5b5f9-197">在 HDInsight 中建立 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="5b5f9-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="5b5f9-198">開始在 HDInsight 中搭配使用 HBase 與 Hadoop</span><span class="sxs-lookup"><span data-stu-id="5b5f9-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="5b5f9-199">使用 HDInsight 中的 HBase 分析 Twitter 情緒</span><span class="sxs-lookup"><span data-stu-id="5b5f9-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="5b5f9-200">[虛擬網路概觀][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="5b5f9-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Hello 新 HBase 叢集的佈建詳細資料"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "使用指令碼動作 toocustomize HBase 叢集"

[azure-preview-portal]: https://portal.azure.com
