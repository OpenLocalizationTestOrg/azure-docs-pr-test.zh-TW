---
title: "在 HDInsight 中的 Hadoop 叢集上使用空白邊緣節點 - Azure | Microsoft Docs"
description: "如何將空白邊緣節點新增至可作為用戶端的 HDInsight 叢集，然後測試/主控 HDInsight 應用程式。"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: e21dabcc6999b1f1047d334e782f723d0c03c2cb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="94bfd-103">在 HDInsight 中的 Hadoop 叢集上使用空白邊緣節點</span><span class="sxs-lookup"><span data-stu-id="94bfd-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="94bfd-104">了解如何將空白邊緣節點新增至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-104">Learn how to add an empty edge node to an HDInsight cluster.</span></span> <span data-ttu-id="94bfd-105">空白邊緣節點是一部 Linux 虛擬機器，其中已安裝及設定和前端節點相同的用戶端工具，但未執行任何 Hadoop 服務。</span><span class="sxs-lookup"><span data-stu-id="94bfd-105">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="94bfd-106">您可以使用邊緣節點來存取叢集、測試用戶端應用程式，以及裝載用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="94bfd-106">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="94bfd-107">您可以將空白邊緣節點新增至現有 HDInsight 叢集，以及在建立叢集時新增到新的叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-107">You can add an empty edge node to an existing HDInsight cluster, to a new cluster when you create the cluster.</span></span> <span data-ttu-id="94bfd-108">空白邊緣節點是使用 Azure Resource Manager 範本來新增。</span><span class="sxs-lookup"><span data-stu-id="94bfd-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="94bfd-109">下列範例示範如何使用範本來新增︰</span><span class="sxs-lookup"><span data-stu-id="94bfd-109">The following sample demonstrates how it is done using a template:</span></span>

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

<span data-ttu-id="94bfd-110">如範例所示，您可以選擇性地呼叫[指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)來執行其他設定，例如在邊緣節點中安裝 [Apache Hue](hdinsight-hadoop-hue-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-110">As shown in the sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) to perform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in the edge node.</span></span> <span data-ttu-id="94bfd-111">指令碼動作指令碼必須可在網站上公開存取。</span><span class="sxs-lookup"><span data-stu-id="94bfd-111">The script action script must be publicly accessible on the web.</span></span>  <span data-ttu-id="94bfd-112">例如，如果指令碼儲存在 Azure 儲存體中，則需使用公用容器或公用 Blob。</span><span class="sxs-lookup"><span data-stu-id="94bfd-112">For example, if the script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="94bfd-113">邊緣節點虛擬機器大小必須符合 HDInsight 叢集背景工作節點 VM 大小需求。</span><span class="sxs-lookup"><span data-stu-id="94bfd-113">The edge node virtual machine size must meet the HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="94bfd-114">如需建議的背景工作節點 VM 大小，請參閱[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-114">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="94bfd-115">建立邊緣節點之後，您可以使用 SSH 連線到邊緣節點，並執行用戶端工具來存取 HDInsight 中的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-115">After you have created an edge node, you can connect to the edge node using SSH, and run client tools to access the Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="94bfd-116">搭配 HDInsight 使用空白邊緣節點目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="94bfd-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="94bfd-117">邊緣節點上安裝的自訂元件會收到來自 Microsoft 的商業上合理支援。</span><span class="sxs-lookup"><span data-stu-id="94bfd-117">Custom components that are installed on the edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="94bfd-118">可能可以解決您遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="94bfd-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="94bfd-119">或者，您可能需要參考社群資源以取得進一步協助。</span><span class="sxs-lookup"><span data-stu-id="94bfd-119">Or you may be referred to community resources for further assistance.</span></span> <span data-ttu-id="94bfd-120">以下是從社群取得協助的一些最活躍網站：</span><span class="sxs-lookup"><span data-stu-id="94bfd-120">The following are some of the most active sites for getting help from the community:</span></span>
>
> * [<span data-ttu-id="94bfd-121">HDInsight 的 MSDN 論壇</span><span class="sxs-lookup"><span data-stu-id="94bfd-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="94bfd-122">[http://stackoverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="94bfd-123">如果您使用 Apache 技術，您可以透過位於 [http://apache.org](http://apache.org) 的 Apache 專案網站 (例如 [Hadoop](http://hadoop.apache.org/) 網站) 找到協助。</span><span class="sxs-lookup"><span data-stu-id="94bfd-123">If you are using an Apache technology, you may be able to find assistance through the Apache project sites on [http://apache.org](http://apache.org), such as the [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-to-an-existing-cluster"></a><span data-ttu-id="94bfd-124">將邊緣節點新增至現有叢集</span><span class="sxs-lookup"><span data-stu-id="94bfd-124">Add an edge node to an existing cluster</span></span>
<span data-ttu-id="94bfd-125">在本節中，您會使用 Resource Manager 範本將邊緣節點新增至現有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-125">In this section, you use a Resource Manager template to add an edge node to an existing HDInsight cluster.</span></span>  <span data-ttu-id="94bfd-126">Resource Manager 範本可在 [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/)中找到。</span><span class="sxs-lookup"><span data-stu-id="94bfd-126">The Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="94bfd-127">Resource Manager 範本會呼叫位於 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh 的指令碼動作。此指令碼不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="94bfd-127">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="94bfd-128">其目的只是為了示範從 Resource Manager 範本呼叫指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="94bfd-128">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="94bfd-129">**將空白邊緣節點新增至現有叢集**</span><span class="sxs-lookup"><span data-stu-id="94bfd-129">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="94bfd-130">如果您還沒有 HDInsight 叢集，請予以建立。</span><span class="sxs-lookup"><span data-stu-id="94bfd-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="94bfd-131">請參閱[Hadoop 教學課程：開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="94bfd-132">按一下以下影像，在 Azure 入口網站中登入 Azure 並開啟 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="94bfd-132">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="94bfd-133">設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="94bfd-133">Configure the following properties:</span></span>
   
   * <span data-ttu-id="94bfd-134">**訂用帳戶**：選取用來建立叢集的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="94bfd-134">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="94bfd-135">**資源群組**：選取用於現有 HDInsight 叢集的資源群組。</span><span class="sxs-lookup"><span data-stu-id="94bfd-135">**Resource group**: Select the resource group used for the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="94bfd-136">**位置**：選取現有 HDInsight 叢集的位置。</span><span class="sxs-lookup"><span data-stu-id="94bfd-136">**Location**: Select the location of the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="94bfd-137">**叢集名稱**︰輸入現有 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="94bfd-137">**Cluster Name**: Enter the name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="94bfd-138">**邊緣節點大小**︰選取其中一個 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="94bfd-138">**Edge Node Size**: Select one of the VM sizes.</span></span> <span data-ttu-id="94bfd-139">VM 大小必須符合背景工作節點 VM 大小需求。</span><span class="sxs-lookup"><span data-stu-id="94bfd-139">The vm size must meet the worker node vm size requirements.</span></span> <span data-ttu-id="94bfd-140">如需建議的背景工作節點 VM 大小，請參閱[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-140">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="94bfd-141">**邊緣節點前置詞**︰預設值是 **new**。</span><span class="sxs-lookup"><span data-stu-id="94bfd-141">**Edge Node Prefix**: The default value is **new**.</span></span>  <span data-ttu-id="94bfd-142">若使用預設值，邊緣節點名稱是 **new-edgenode**。</span><span class="sxs-lookup"><span data-stu-id="94bfd-142">Using the default value, the edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="94bfd-143">您可以從入口網站自訂前置詞。</span><span class="sxs-lookup"><span data-stu-id="94bfd-143">You can customize the prefix from the portal.</span></span> <span data-ttu-id="94bfd-144">您也可以從範本自訂完整名稱。</span><span class="sxs-lookup"><span data-stu-id="94bfd-144">You can also customize the full name from the template.</span></span>

4. <span data-ttu-id="94bfd-145">核取 [我同意上方所述的條款及條件]，然後按一下 [購買] 以建立邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="94bfd-145">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="94bfd-146">請務必選取用於現有 HDInsight 叢集的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="94bfd-146">Make sure to select the Azure resource group for the existing HDInsight cluster.</span></span>  <span data-ttu-id="94bfd-147">否則，您會收到錯誤訊息：「無法對巢狀資源執行所要求的作業。</span><span class="sxs-lookup"><span data-stu-id="94bfd-147">Otherwise, you get the error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="94bfd-148">找不到父資源 '&lt;叢集名稱>'」。</span><span class="sxs-lookup"><span data-stu-id="94bfd-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="94bfd-149">在建立叢集時新增邊緣節點</span><span class="sxs-lookup"><span data-stu-id="94bfd-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="94bfd-150">在本節中，您會使用 Resource Manager 範本對邊緣節點建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-150">In this section, you use a Resource Manager template to create HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="94bfd-151">Resource Manager 範本可在 [Azure 快速入門範本資源庫](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/)中找到。</span><span class="sxs-lookup"><span data-stu-id="94bfd-151">The Resource Manager template can be found in the [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="94bfd-152">Resource Manager 範本會呼叫位於 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh 的指令碼動作。此指令碼不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="94bfd-152">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="94bfd-153">其目的只是為了示範從 Resource Manager 範本呼叫指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="94bfd-153">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="94bfd-154">**將空白邊緣節點新增至現有叢集**</span><span class="sxs-lookup"><span data-stu-id="94bfd-154">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="94bfd-155">如果您還沒有 HDInsight 叢集，請予以建立。</span><span class="sxs-lookup"><span data-stu-id="94bfd-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="94bfd-156">請參閱[開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="94bfd-157">按一下以下影像，在 Azure 入口網站中登入 Azure 並開啟 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="94bfd-157">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="94bfd-158">設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="94bfd-158">Configure the following properties:</span></span>
   
   * <span data-ttu-id="94bfd-159">**訂用帳戶**：選取用來建立叢集的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="94bfd-159">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="94bfd-160">**資源群組**：建立用於叢集的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="94bfd-160">**Resource group**: Create a new resource group used for the cluster.</span></span>
   * <span data-ttu-id="94bfd-161">**位置**：選取資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="94bfd-161">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="94bfd-162">**叢集名稱**︰輸入要建立之新叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="94bfd-162">**Cluster Name**: Enter a name for the new cluster to create.</span></span>
   * <span data-ttu-id="94bfd-163">**叢集登入使用者名稱**︰輸入 Hadoop HTTP 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="94bfd-163">**Cluster Login User Name**: Enter the Hadoop HTTP user name.</span></span>  <span data-ttu-id="94bfd-164">預設名稱為 **admin**。</span><span class="sxs-lookup"><span data-stu-id="94bfd-164">The default name is **admin**.</span></span>
   * <span data-ttu-id="94bfd-165">**叢集登入密碼**︰輸入 Hadoop HTTP 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="94bfd-165">**Cluster Login Password**: Enter the Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="94bfd-166">**SSH 使用者名稱**︰輸入 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="94bfd-166">**Ssh User Name**: Enter the SSH user name.</span></span> <span data-ttu-id="94bfd-167">預設名稱為 **sshuser**。</span><span class="sxs-lookup"><span data-stu-id="94bfd-167">The default name is **sshuser**.</span></span>
   * <span data-ttu-id="94bfd-168">**SSH 密碼**︰輸入 SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="94bfd-168">**Ssh Password**: Enter the SSH user password.</span></span>
   * <span data-ttu-id="94bfd-169">**安裝指令碼動作**︰請保留預設值以便完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="94bfd-169">**Install Script Action**: Keep the default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="94bfd-170">某些屬性已被硬式編碼在範本中︰叢集類型、叢集背景工作角色節點計數、邊緣節點大小與邊緣節點名稱。</span><span class="sxs-lookup"><span data-stu-id="94bfd-170">Some properties have been hardcoded in the template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="94bfd-171">核取 [我同意上方所述的條款及條件]，然後按一下 [購買] 以建立具有邊緣節點的叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-171">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the cluster with the edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="94bfd-172">存取邊緣節點</span><span class="sxs-lookup"><span data-stu-id="94bfd-172">Access an edge node</span></span>
<span data-ttu-id="94bfd-173">邊緣節點 ssh 端點是 &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22。</span><span class="sxs-lookup"><span data-stu-id="94bfd-173">The edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="94bfd-174">例如，new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22。</span><span class="sxs-lookup"><span data-stu-id="94bfd-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="94bfd-175">在 Azure 入口網站上，邊緣節點會顯示為應用程式。</span><span class="sxs-lookup"><span data-stu-id="94bfd-175">The edge node appears as an application on the Azure portal.</span></span>  <span data-ttu-id="94bfd-176">入口網站可提供您相關資訊，以便使用 SSH 存取邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="94bfd-176">The portal gives you the information to access the edge node using SSH.</span></span>

<span data-ttu-id="94bfd-177">**確認邊緣節點 SSH 端點**</span><span class="sxs-lookup"><span data-stu-id="94bfd-177">**To verify the edge node SSH endpoint**</span></span>

1. <span data-ttu-id="94bfd-178">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-178">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="94bfd-179">開啟具有邊緣節點的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-179">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="94bfd-180">從叢集刀鋒視窗中，按一下 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="94bfd-180">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="94bfd-181">您應該會看到邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="94bfd-181">You shall see the edge node.</span></span>  <span data-ttu-id="94bfd-182">預設名稱為 **new-edgenode**中找到。</span><span class="sxs-lookup"><span data-stu-id="94bfd-182">The default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="94bfd-183">按一下邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="94bfd-183">Click the edge node.</span></span> <span data-ttu-id="94bfd-184">您應該會看到 SSH 端點。</span><span class="sxs-lookup"><span data-stu-id="94bfd-184">You shall see the SSH endpoint.</span></span>

<span data-ttu-id="94bfd-185">**在邊緣節點上使用 Hive**</span><span class="sxs-lookup"><span data-stu-id="94bfd-185">**To use Hive on the edge node**</span></span>

1. <span data-ttu-id="94bfd-186">使用 SSH 連線到邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="94bfd-186">Use SSH to connect to the edge node.</span></span> <span data-ttu-id="94bfd-187">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="94bfd-188">在使用 SSH 連線到邊緣節點之後，使用下列命令來開啟 Hive 主控台︰</span><span class="sxs-lookup"><span data-stu-id="94bfd-188">After you have connected to the edge node using SSH, use the following command to open the Hive console:</span></span>
   
        hive
3. <span data-ttu-id="94bfd-189">執行下列命令，以顯示叢集中的 Hive 資料表︰</span><span class="sxs-lookup"><span data-stu-id="94bfd-189">Run the following command to show Hive tables in the cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="94bfd-190">刪除邊緣節點</span><span class="sxs-lookup"><span data-stu-id="94bfd-190">Delete an edge node</span></span>
<span data-ttu-id="94bfd-191">您可以從 Azure 入口網站刪除邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="94bfd-191">You can delete an edge node from the Azure portal.</span></span>

<span data-ttu-id="94bfd-192">**存取邊緣節點**</span><span class="sxs-lookup"><span data-stu-id="94bfd-192">**To access an edge node**</span></span>

1. <span data-ttu-id="94bfd-193">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="94bfd-193">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="94bfd-194">開啟具有邊緣節點的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-194">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="94bfd-195">從叢集刀鋒視窗中，按一下 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="94bfd-195">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="94bfd-196">您應該會看到邊緣節點清單。</span><span class="sxs-lookup"><span data-stu-id="94bfd-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="94bfd-197">以滑鼠右鍵按一下您想要刪除的邊緣節點，然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="94bfd-197">Right-click the edge node you want to delete, and then click **Delete**.</span></span>
5. <span data-ttu-id="94bfd-198">按一下 [ **是** ] 以確認。</span><span class="sxs-lookup"><span data-stu-id="94bfd-198">Click **Yes** to confirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94bfd-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94bfd-199">Next steps</span></span>
<span data-ttu-id="94bfd-200">在本文中，您已了解如何新增邊緣節點以及如何存取邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="94bfd-200">In this article, you have learned how to add an edge node and how to access the edge node.</span></span> <span data-ttu-id="94bfd-201">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="94bfd-201">To learn more, see the following articles:</span></span>

* <span data-ttu-id="94bfd-202">[安裝 HDInsight 應用程式](hdinsight-apps-install-applications.md)︰了解如何將 HDInsight 應用程式安裝到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="94bfd-203">[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)︰了解如何將未發佈的 HDInsight 應用程式部署到 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="94bfd-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="94bfd-204">[發佈 HDInsight 應用程式](hdinsight-apps-publish-applications.md)︰了解如何將自訂 HDInsight 應用程式發佈至 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="94bfd-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="94bfd-205">[MSDN：安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)︰了解如何定義 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="94bfd-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="94bfd-206">[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)：了解如何使用指令碼動作來安裝其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="94bfd-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="94bfd-207">[使用 Resource Manager 範本在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)︰了解如何呼叫 Resource Manager 範本來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="94bfd-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>

