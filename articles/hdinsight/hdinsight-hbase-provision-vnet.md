---
title: "在虛擬網路上建立 HBase 叢集 - Azure | Microsoft Docs"
description: "開始在 Azure HDInsight 中使用 HBase。 了解如何在 Azure 虛擬網路上建立 HDInsight HBase 叢集。"
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
ms.openlocfilehash: 668bd494ce3274188af56cf7d6253cec7af9abbc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="fcd93-104">在 Azure 虛擬網路的 HDInsight 上建立 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="fcd93-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="fcd93-105">了解如何在 [Azure 虛擬網路][1]中建立 Azure HDInsight HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="fcd93-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="fcd93-106">由於 HBase 叢集已與虛擬網路整合，因此能夠部署到與您應用程式相同的虛擬網路，讓應用程式得以和 HBase 直接通訊。</span><span class="sxs-lookup"><span data-stu-id="fcd93-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="fcd93-107">其優點包括：</span><span class="sxs-lookup"><span data-stu-id="fcd93-107">The benefits include:</span></span>

* <span data-ttu-id="fcd93-108">Web 應用程式可以直接連接到 HBase 叢集節點，因而能夠使用 HBase Java 遠端程序呼叫 (RPC) API 來進行通訊。</span><span class="sxs-lookup"><span data-stu-id="fcd93-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="fcd93-109">透過使流量不須經過多個閘道器及負載平衡器，以提升其效能。</span><span class="sxs-lookup"><span data-stu-id="fcd93-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="fcd93-110">能夠以更安全的方式處理敏感資訊，而不會暴露公用端點。</span><span class="sxs-lookup"><span data-stu-id="fcd93-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fcd93-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="fcd93-111">Prerequisites</span></span>
<span data-ttu-id="fcd93-112">開始進行本教學課程之前，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="fcd93-112">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="fcd93-113">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fcd93-113">**An Azure subscription**.</span></span> <span data-ttu-id="fcd93-114">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="fcd93-115">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="fcd93-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="fcd93-116">請參閱 [安裝及使用 Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="fcd93-117">在虛擬網路上建立 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="fcd93-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="fcd93-118">在本節中，您會使用 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)，在 Azure 虛擬網路中建立以 Linux 為基礎的 HBase 叢集與相依的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcd93-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="fcd93-119">如需其他叢集建立方法及了解各項設定，請參閱 [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="fcd93-120">如需有關使用範本在 HDInsight 中建立 Hadoop 叢集的詳細資訊，請參閱 [使用 Azure Resource Manager 範本在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="fcd93-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="fcd93-121">某些屬性已以硬式編碼方式寫入範本。</span><span class="sxs-lookup"><span data-stu-id="fcd93-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="fcd93-122">例如：</span><span class="sxs-lookup"><span data-stu-id="fcd93-122">For example:</span></span>
>
> * <span data-ttu-id="fcd93-123">**位置**：美國東部 2</span><span class="sxs-lookup"><span data-stu-id="fcd93-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="fcd93-124">**叢集版本**：3.5</span><span class="sxs-lookup"><span data-stu-id="fcd93-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="fcd93-125">**叢集背景工作節點計數**：2</span><span class="sxs-lookup"><span data-stu-id="fcd93-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="fcd93-126">**預設儲存體帳戶**：唯一的字串</span><span class="sxs-lookup"><span data-stu-id="fcd93-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="fcd93-127">**虛擬網路名稱**：&lt;叢集名稱>-vnet</span><span class="sxs-lookup"><span data-stu-id="fcd93-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="fcd93-128">**虛擬網路位址空間**10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="fcd93-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="fcd93-129">**子網路名稱**：subnet1</span><span class="sxs-lookup"><span data-stu-id="fcd93-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="fcd93-130">**子網路位址範圍**：10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="fcd93-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="fcd93-131">使用範本時，&lt;叢集名稱> 會取代為您提供的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="fcd93-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="fcd93-132">按一下以下影像，在 Azure 入口網站中開啟範本。</span><span class="sxs-lookup"><span data-stu-id="fcd93-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="fcd93-133">範本位在 [Azure 快速入門範本 (英文)](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="fcd93-134">從 [自訂部署] 刀鋒視窗中，輸入下列屬性：</span><span class="sxs-lookup"><span data-stu-id="fcd93-134">From the **Custom deployment** blade, enter the following properties:</span></span>

   * <span data-ttu-id="fcd93-135">**訂用帳戶**︰選取用來建立 HDInsight 叢集、相依儲存體帳戶和 Azure 虛擬網路的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcd93-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="fcd93-136">**資源群組**：選取 [新建] 並指定新的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="fcd93-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="fcd93-137">**位置**：選取資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="fcd93-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="fcd93-138">**ClusterName**：輸入要建立的 Hadoop 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="fcd93-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="fcd93-139">**叢集登入名稱和密碼**：預設登入名稱是 **admin**。</span><span class="sxs-lookup"><span data-stu-id="fcd93-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="fcd93-140">**SSH 使用者名稱和密碼**：預設使用者名稱是 **sshuser**。</span><span class="sxs-lookup"><span data-stu-id="fcd93-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="fcd93-141">您可以將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="fcd93-141">You can rename it.</span></span>
   * <span data-ttu-id="fcd93-142">**我同意上方所述的條款及條件**：(選取)</span><span class="sxs-lookup"><span data-stu-id="fcd93-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="fcd93-143">按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="fcd93-143">Click **Purchase**.</span></span> <span data-ttu-id="fcd93-144">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="fcd93-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="fcd93-145">一旦建立叢集後，您可以在入口網站按一下 [叢集] 刀鋒視窗來開啟它。</span><span class="sxs-lookup"><span data-stu-id="fcd93-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="fcd93-146">完成本教學課程之後，您可以刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="fcd93-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="fcd93-147">利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。</span><span class="sxs-lookup"><span data-stu-id="fcd93-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="fcd93-148">您也需支付 HDInsight 叢集的費用 (即使未使用)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="fcd93-149">由於叢集費用是儲存體費用的許多倍，所以刪除未使用的叢集符合經濟效益。</span><span class="sxs-lookup"><span data-stu-id="fcd93-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="fcd93-150">如需有關刪除叢集的指示，請參閱[使用 Azure 入口網站管理 HDInsight 中的 Hadoop 叢集](hdinsight-administer-use-management-portal.md#delete-clusters)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="fcd93-151">若要開始使用新的 HBase 叢集，您可以使用＜ [開始在 HDInsight 中搭配使用 HBase 與 Hadoop](hdinsight-hbase-tutorial-get-started.md)＞中提供的程序。</span><span class="sxs-lookup"><span data-stu-id="fcd93-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="fcd93-152">使用 HBase Java RPC API 連接到 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="fcd93-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="fcd93-153">相同的 Azure 虛擬網路和相同的子網路中建立基礎結構即服務 (IaaS) 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fcd93-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="fcd93-154">如需建立新的 IaaS 虛擬機器的指示，請參閱[建立執行 Windows Server 的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="fcd93-155">當遵循本文件中的步驟時，您必須針對網路設定使用下列值：</span><span class="sxs-lookup"><span data-stu-id="fcd93-155">When following the steps in this document, you must use the following values for the Network configuration:</span></span>

   * <span data-ttu-id="fcd93-156">**虛擬網路**：&lt;叢集名稱>-vnet</span><span class="sxs-lookup"><span data-stu-id="fcd93-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="fcd93-157">**子網路**：subnet1</span><span class="sxs-lookup"><span data-stu-id="fcd93-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="fcd93-158">將 &lt;叢集名稱> 取代為在上一個步驟中建立 HDInsight 叢集時使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="fcd93-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="fcd93-159">使用這些值會將虛擬機器放置在與 HDInsight 叢集相同的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="fcd93-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="fcd93-160">此組態可讓它們彼此直接通訊。</span><span class="sxs-lookup"><span data-stu-id="fcd93-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="fcd93-161">有一個使用空白邊緣節點建立 HDInsight 叢集的方法。</span><span class="sxs-lookup"><span data-stu-id="fcd93-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="fcd93-162">邊緣節點可用來管理叢集。</span><span class="sxs-lookup"><span data-stu-id="fcd93-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="fcd93-163">如需詳細資訊，請參閱 [Use empty edge nodes in HDInsight (在 HDInsight 中使用空白的邊緣節點)](hdinsight-apps-use-edge-node.md)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="fcd93-164">使用 Java 應用程式從遠端連接到 HBase 時，您必須使用完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="fcd93-165">若要決定此名稱，您必須取得 HBase 叢集的連線特定 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="fcd93-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="fcd93-166">若要這麼做，您可以使用下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="fcd93-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="fcd93-167">使用網頁瀏覽器進行 Ambari 呼叫︰</span><span class="sxs-lookup"><span data-stu-id="fcd93-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="fcd93-168">瀏覽至 https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true。</span><span class="sxs-lookup"><span data-stu-id="fcd93-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="fcd93-169">結果是具有 DNS 尾碼的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcd93-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="fcd93-170">使用 Ambari 網站︰</span><span class="sxs-lookup"><span data-stu-id="fcd93-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="fcd93-171">瀏覽至 https://&lt;ClusterName>.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="fcd93-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="fcd93-172">按一下頂端功能表中的 [主機]  。</span><span class="sxs-lookup"><span data-stu-id="fcd93-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="fcd93-173">使用 Curl 進行 REST 呼叫︰</span><span class="sxs-lookup"><span data-stu-id="fcd93-173">Use Curl to make REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="fcd93-174">在傳回的 JavaScript 物件標記法 (JSON) 資料中，找出 "host_name" 項目。</span><span class="sxs-lookup"><span data-stu-id="fcd93-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="fcd93-175">其中包含叢集中節點的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="fcd93-175">It contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="fcd93-176">例如：</span><span class="sxs-lookup"><span data-stu-id="fcd93-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="fcd93-177">以叢集名稱開頭的網域名稱部分就是 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="fcd93-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="fcd93-178">例如，mycluster.b1.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="fcd93-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="fcd93-179">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcd93-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="fcd93-180">使用下列 Azure PowerShell 指令碼來註冊 **Get-ClusterDetail** 函數，此函數可用來傳回 DNS 尾碼：</span><span class="sxs-lookup"><span data-stu-id="fcd93-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

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
            Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
            .Description
            This command shows the following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run the HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows the FQDN suffix of hosts in the cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows the value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run the HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows the FQDN suffix of hosts in the cluster.
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

     <span data-ttu-id="fcd93-181">執行 Azure PowerShell 指令碼之後，透過下列命令使用 **Get-ClusterDetail** 函數傳回 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="fcd93-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="fcd93-182">使用此命令時，請指定您的 HDInsight HBase 叢集名稱、管理員名稱和管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="fcd93-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="fcd93-183">此命令會傳回 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="fcd93-183">This command returns the DNS suffix.</span></span> <span data-ttu-id="fcd93-184">例如， **yourclustername.b4.internal.cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="fcd93-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="fcd93-185">若要驗證虛擬機器能夠與 HBase 叢集通訊，請從虛擬機器使用命令 `ping headnode0.<dns suffix>` 。</span><span class="sxs-lookup"><span data-stu-id="fcd93-185">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="fcd93-186">例如，ping headnode0.mycluster.b1.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="fcd93-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="fcd93-187">若要在 Java 應用程式中使用此資訊，您可以依照＜ [使用 Maven 建置在 HDInsight (Hadoop) 上使用 HBase 的 Java 應用程式](hdinsight-hbase-build-java-maven.md) ＞(英文) 中的步驟來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcd93-187">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="fcd93-188">若要讓應用程式連接到遠端 HBase 伺服器，請修改此範例中的 **hbase-site.xml** 檔案，以使用 Zookeeper 的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="fcd93-188">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="fcd93-189">例如：</span><span class="sxs-lookup"><span data-stu-id="fcd93-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="fcd93-190">如需 Azure 虛擬網路中名稱解析的詳細資訊，包括如何使用您自己的 DNS 伺服器，請參閱[名稱解析 (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="fcd93-190">For more information about name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="fcd93-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fcd93-191">Next steps</span></span>
<span data-ttu-id="fcd93-192">在本教學課程中，您已了解如何建立 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="fcd93-192">In this tutorial, you learned how to create an HBase cluster.</span></span> <span data-ttu-id="fcd93-193">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="fcd93-193">To learn more, see:</span></span>

* [<span data-ttu-id="fcd93-194">開始使用 HDInsight</span><span class="sxs-lookup"><span data-stu-id="fcd93-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="fcd93-195">在 HDInsight 中使用空白邊緣節點</span><span class="sxs-lookup"><span data-stu-id="fcd93-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="fcd93-196">在 HDInsight 中設定 HBase 複寫</span><span class="sxs-lookup"><span data-stu-id="fcd93-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="fcd93-197">在 HDInsight 中建立 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="fcd93-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="fcd93-198">開始在 HDInsight 中搭配使用 HBase 與 Hadoop</span><span class="sxs-lookup"><span data-stu-id="fcd93-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="fcd93-199">使用 HDInsight 中的 HBase 分析 Twitter 情緒</span><span class="sxs-lookup"><span data-stu-id="fcd93-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="fcd93-200">[虛擬網路概觀][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="fcd93-200">[Virtual Network Overview][vnet-overview]</span></span>

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
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "佈建新 HBase 叢集的詳細資料"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "使用指令碼動作以自訂 HBase 叢集"

[azure-preview-portal]: https://portal.azure.com
