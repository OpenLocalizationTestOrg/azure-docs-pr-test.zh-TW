---
title: "aaaUse 空 HDInsight 的 Azure 中的 Hadoop 叢集上的邊緣節點 |Microsoft 文件"
description: "如何 tooadd 空白邊緣節點 tooan HDInsight 叢集的可用做為用戶端，然後測試/主機 HDInsight 應用程式。"
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
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="920da-103">在 HDInsight 中的 Hadoop 叢集上使用空白邊緣節點</span><span class="sxs-lookup"><span data-stu-id="920da-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="920da-104">了解如何 tooadd 空白邊緣節點 tooan HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-104">Learn how tooadd an empty edge node tooan HDInsight cluster.</span></span> <span data-ttu-id="920da-105">空白邊緣節點是在 Linux 虛擬機器具有相同的用戶端工具安裝並設定與 hello headnodes hello，但 Hadoop 服務執行。</span><span class="sxs-lookup"><span data-stu-id="920da-105">An empty edge node is a Linux virtual machine with hello same client tools installed and configured as in hello headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="920da-106">您可以使用 hello 邊緣節點存取 hello 叢集、 測試用戶端應用程式，以及裝載用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="920da-106">You can use hello edge node for accessing hello cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="920da-107">當您建立 hello 叢集時，您可以新增空白邊緣節點 tooan 現有 HDInsight 叢集、 tooa 新叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-107">You can add an empty edge node tooan existing HDInsight cluster, tooa new cluster when you create hello cluster.</span></span> <span data-ttu-id="920da-108">空白邊緣節點是使用 Azure Resource Manager 範本來新增。</span><span class="sxs-lookup"><span data-stu-id="920da-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="920da-109">hello 下列範例將示範如何完成使用範本：</span><span class="sxs-lookup"><span data-stu-id="920da-109">hello following sample demonstrates how it is done using a template:</span></span>

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

<span data-ttu-id="920da-110">Hello 範例所示，您可以選擇呼叫[指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)tooperform 額外的設定，例如安裝[Apache 色調](hdinsight-hadoop-hue-linux.md)hello 邊緣節點中。</span><span class="sxs-lookup"><span data-stu-id="920da-110">As shown in hello sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) tooperform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in hello edge node.</span></span> <span data-ttu-id="920da-111">hello 指令碼動作的指令碼必須可公開存取 hello 網站上。</span><span class="sxs-lookup"><span data-stu-id="920da-111">hello script action script must be publicly accessible on hello web.</span></span>  <span data-ttu-id="920da-112">例如，如果 hello 指令碼儲存在 Azure 儲存體中，使用公用容器或公用 blob。</span><span class="sxs-lookup"><span data-stu-id="920da-112">For example, if hello script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="920da-113">hello 邊緣節點的虛擬機器大小必須符合 hello HDInsight 叢集背景工作節點 vm 大小需求。</span><span class="sxs-lookup"><span data-stu-id="920da-113">hello edge node virtual machine size must meet hello HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="920da-114">Hello 建議背景工作節點的 vm 大小，請參閱[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。</span><span class="sxs-lookup"><span data-stu-id="920da-114">For hello recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="920da-115">建立邊緣節點之後，您可以 toohello 邊緣節點使用 SSH 的連接，並在 HDInsight 中執行用戶端工具 tooaccess hello Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-115">After you have created an edge node, you can connect toohello edge node using SSH, and run client tools tooaccess hello Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="920da-116">搭配 HDInsight 使用空白邊緣節點目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="920da-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="920da-117">Hello 邊緣節點已安裝的自訂元件會從 Microsoft 接收盡商業上合理的支援。</span><span class="sxs-lookup"><span data-stu-id="920da-117">Custom components that are installed on hello edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="920da-118">可能可以解決您遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="920da-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="920da-119">或者，您可能需要進一步的協助參照的 toocommunity 資源。</span><span class="sxs-lookup"><span data-stu-id="920da-119">Or you may be referred toocommunity resources for further assistance.</span></span> <span data-ttu-id="920da-120">hello 以下是 hello 的一些取得大部分的作用中網站協助 hello 社群中:</span><span class="sxs-lookup"><span data-stu-id="920da-120">hello following are some of hello most active sites for getting help from hello community:</span></span>
>
> * [<span data-ttu-id="920da-121">HDInsight 的 MSDN 論壇</span><span class="sxs-lookup"><span data-stu-id="920da-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="920da-122">[http://stackoverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="920da-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="920da-123">如果您使用 Apache 技術，您可能無法 toofind 協助 hello 透過 Apache 專案網站上的[http://apache.org](http://apache.org)，例如 hello [Hadoop](http://hadoop.apache.org/)站台。</span><span class="sxs-lookup"><span data-stu-id="920da-123">If you are using an Apache technology, you may be able toofind assistance through hello Apache project sites on [http://apache.org](http://apache.org), such as hello [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-tooan-existing-cluster"></a><span data-ttu-id="920da-124">將邊緣節點 tooan 現有叢集新增</span><span class="sxs-lookup"><span data-stu-id="920da-124">Add an edge node tooan existing cluster</span></span>
<span data-ttu-id="920da-125">在本節中，您可以使用資源管理員範本 tooadd 邊緣節點 tooan 現有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-125">In this section, you use a Resource Manager template tooadd an edge node tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="920da-126">hello Resource Manager 範本位於[GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/)。</span><span class="sxs-lookup"><span data-stu-id="920da-126">hello Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="920da-127">hello Resource Manager 範本呼叫位於 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh 指令碼動作。hello 指令碼不執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="920da-127">hello Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. hello script doesn't perform any actions.</span></span>  <span data-ttu-id="920da-128">它是 toodemonstrate Resource Manager 範本從呼叫的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="920da-128">It is toodemonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="920da-129">**tooadd 空白邊緣節點 tooan 現有叢集**</span><span class="sxs-lookup"><span data-stu-id="920da-129">**tooadd an empty edge node tooan existing cluster**</span></span>

1. <span data-ttu-id="920da-130">如果您還沒有 HDInsight 叢集，請予以建立。</span><span class="sxs-lookup"><span data-stu-id="920da-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="920da-131">請參閱[Hadoop 教學課程：開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="920da-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="920da-132">按一下下列 tooAzure 中的映像 toosign 和開啟 hello Azure Resource Manager 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="920da-132">Click hello following image toosign in tooAzure and open hello Azure Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. <span data-ttu-id="920da-133">設定下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="920da-133">Configure hello following properties:</span></span>
   
   * <span data-ttu-id="920da-134">**訂用帳戶**： 選取用於建立 hello 叢集的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="920da-134">**Subscription**: Select an Azure subscription used for creating hello cluster.</span></span>
   * <span data-ttu-id="920da-135">**資源群組**: hello 選取資源群組用於 hello 現有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-135">**Resource group**: Select hello resource group used for hello existing HDInsight cluster.</span></span>
   * <span data-ttu-id="920da-136">**位置**： 選取 hello 位置 hello 現有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-136">**Location**: Select hello location of hello existing HDInsight cluster.</span></span>
   * <span data-ttu-id="920da-137">**叢集名稱**： 輸入 hello 現有 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="920da-137">**Cluster Name**: Enter hello name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="920da-138">**邊緣節點大小**： 選取其中一個 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="920da-138">**Edge Node Size**: Select one of hello VM sizes.</span></span> <span data-ttu-id="920da-139">hello vm 大小必須符合 hello 背景工作節點的 vm 大小需求。</span><span class="sxs-lookup"><span data-stu-id="920da-139">hello vm size must meet hello worker node vm size requirements.</span></span> <span data-ttu-id="920da-140">Hello 建議背景工作節點的 vm 大小，請參閱[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。</span><span class="sxs-lookup"><span data-stu-id="920da-140">For hello recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="920da-141">**邊緣節點的前置詞**: hello 預設值是**新**。</span><span class="sxs-lookup"><span data-stu-id="920da-141">**Edge Node Prefix**: hello default value is **new**.</span></span>  <span data-ttu-id="920da-142">使用 hello 預設值，hello 邊緣節點名稱是**新 edgenode**。</span><span class="sxs-lookup"><span data-stu-id="920da-142">Using hello default value, hello edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="920da-143">您可以自訂 hello 從 hello 入口網站的前置詞。</span><span class="sxs-lookup"><span data-stu-id="920da-143">You can customize hello prefix from hello portal.</span></span> <span data-ttu-id="920da-144">您也可以自訂 hello 從 hello 範本的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="920da-144">You can also customize hello full name from hello template.</span></span>

4. <span data-ttu-id="920da-145">請檢查**toohello 條款和條件前面所述，即表示我同意**，然後按一下**購買**toocreate hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="920da-145">Check **I agree toohello terms and conditions stated above**, and then click  **Purchase** toocreate hello edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="920da-146">請確定現有 HDInsight 叢集 hello tooselect hello Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="920da-146">Make sure tooselect hello Azure resource group for hello existing HDInsight cluster.</span></span>  <span data-ttu-id="920da-147">否則，您會收到 hello 錯誤訊息 「 無法執行要求的作業，巢狀資源上。</span><span class="sxs-lookup"><span data-stu-id="920da-147">Otherwise, you get hello error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="920da-148">找不到父資源 '&lt;叢集名稱>'」。</span><span class="sxs-lookup"><span data-stu-id="920da-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="920da-149">在建立叢集時新增邊緣節點</span><span class="sxs-lookup"><span data-stu-id="920da-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="920da-150">在本節中，您可以使用 資源管理員範本 toocreate HDInsight 叢集與邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="920da-150">In this section, you use a Resource Manager template toocreate HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="920da-151">hello Resource Manager 範本可以在 hello [Azure 快速入門範本組件庫](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/)。</span><span class="sxs-lookup"><span data-stu-id="920da-151">hello Resource Manager template can be found in hello [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="920da-152">hello Resource Manager 範本呼叫位於 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh 指令碼動作。hello 指令碼不執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="920da-152">hello Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. hello script doesn't perform any actions.</span></span>  <span data-ttu-id="920da-153">它是 toodemonstrate Resource Manager 範本從呼叫的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="920da-153">It is toodemonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="920da-154">**tooadd 空白邊緣節點 tooan 現有叢集**</span><span class="sxs-lookup"><span data-stu-id="920da-154">**tooadd an empty edge node tooan existing cluster**</span></span>

1. <span data-ttu-id="920da-155">如果您還沒有 HDInsight 叢集，請予以建立。</span><span class="sxs-lookup"><span data-stu-id="920da-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="920da-156">請參閱[開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="920da-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="920da-157">按一下下列 tooAzure 中的映像 toosign 和開啟 hello Azure Resource Manager 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="920da-157">Click hello following image toosign in tooAzure and open hello Azure Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. <span data-ttu-id="920da-158">設定下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="920da-158">Configure hello following properties:</span></span>
   
   * <span data-ttu-id="920da-159">**訂用帳戶**： 選取用於建立 hello 叢集的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="920da-159">**Subscription**: Select an Azure subscription used for creating hello cluster.</span></span>
   * <span data-ttu-id="920da-160">**資源群組**： 建立新的資源群組，用於 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-160">**Resource group**: Create a new resource group used for hello cluster.</span></span>
   * <span data-ttu-id="920da-161">**位置**： 選取 hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="920da-161">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="920da-162">**叢集名稱**： 輸入新叢集 toocreate hello 的名稱。</span><span class="sxs-lookup"><span data-stu-id="920da-162">**Cluster Name**: Enter a name for hello new cluster toocreate.</span></span>
   * <span data-ttu-id="920da-163">**叢集登入使用者名稱**： 輸入 hello Hadoop HTTP 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="920da-163">**Cluster Login User Name**: Enter hello Hadoop HTTP user name.</span></span>  <span data-ttu-id="920da-164">hello 預設名稱是**admin**。</span><span class="sxs-lookup"><span data-stu-id="920da-164">hello default name is **admin**.</span></span>
   * <span data-ttu-id="920da-165">**叢集登入密碼**： 輸入 hello Hadoop HTTP 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="920da-165">**Cluster Login Password**: Enter hello Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="920da-166">**Ssh 使用者名稱**： 輸入 hello SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="920da-166">**Ssh User Name**: Enter hello SSH user name.</span></span> <span data-ttu-id="920da-167">hello 預設名稱是**sshuser**。</span><span class="sxs-lookup"><span data-stu-id="920da-167">hello default name is **sshuser**.</span></span>
   * <span data-ttu-id="920da-168">**Ssh 密碼**： 輸入 hello SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="920da-168">**Ssh Password**: Enter hello SSH user password.</span></span>
   * <span data-ttu-id="920da-169">**安裝指令碼動作**： 保留 hello 預設值將在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="920da-169">**Install Script Action**: Keep hello default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="920da-170">某些屬性已被 hello 範本中的硬式編碼： 叢集類型、 叢集背景工作節點計數、 邊緣節點大小，以及邊緣節點名稱。</span><span class="sxs-lookup"><span data-stu-id="920da-170">Some properties have been hardcoded in hello template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="920da-171">請檢查**toohello 條款和條件前面所述，即表示我同意**，然後按一下**購買**toocreate hello 叢集與 hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="920da-171">Check **I agree toohello terms and conditions stated above**, and then click  **Purchase** toocreate hello cluster with hello edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="920da-172">存取邊緣節點</span><span class="sxs-lookup"><span data-stu-id="920da-172">Access an edge node</span></span>
<span data-ttu-id="920da-173">hello 邊緣節點 ssh 端點是&lt;EdgeNodeName >。&lt;ClusterName >-ssh.azurehdinsight.net:22。</span><span class="sxs-lookup"><span data-stu-id="920da-173">hello edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="920da-174">例如，new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22。</span><span class="sxs-lookup"><span data-stu-id="920da-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="920da-175">hello 邊緣節點會顯示為 hello Azure 入口網站上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="920da-175">hello edge node appears as an application on hello Azure portal.</span></span>  <span data-ttu-id="920da-176">hello 資訊 tooaccess hello hello 入口網站可讓邊緣使用 SSH 的節點。</span><span class="sxs-lookup"><span data-stu-id="920da-176">hello portal gives you hello information tooaccess hello edge node using SSH.</span></span>

<span data-ttu-id="920da-177">**tooverify hello 邊緣節點 SSH 端點**</span><span class="sxs-lookup"><span data-stu-id="920da-177">**tooverify hello edge node SSH endpoint**</span></span>

1. <span data-ttu-id="920da-178">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="920da-178">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="920da-179">與邊緣節點開啟 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-179">Open hello HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="920da-180">按一下**應用程式**從 hello 叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="920da-180">Click **Applications** from hello cluster blade.</span></span> <span data-ttu-id="920da-181">您應該會看到 hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="920da-181">You shall see hello edge node.</span></span>  <span data-ttu-id="920da-182">hello 預設名稱是**新 edgenode**。</span><span class="sxs-lookup"><span data-stu-id="920da-182">hello default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="920da-183">按一下 hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="920da-183">Click hello edge node.</span></span> <span data-ttu-id="920da-184">您應該會看到 hello SSH 的端點。</span><span class="sxs-lookup"><span data-stu-id="920da-184">You shall see hello SSH endpoint.</span></span>

<span data-ttu-id="920da-185">**toouse Hive hello 邊緣節點上**</span><span class="sxs-lookup"><span data-stu-id="920da-185">**toouse Hive on hello edge node**</span></span>

1. <span data-ttu-id="920da-186">使用 SSH tooconnect toohello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="920da-186">Use SSH tooconnect toohello edge node.</span></span> <span data-ttu-id="920da-187">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="920da-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="920da-188">您已經連接使用 SSH toohello 邊緣節點之後，使用下列命令 tooopen hello Hive 主控台中的 hello:</span><span class="sxs-lookup"><span data-stu-id="920da-188">After you have connected toohello edge node using SSH, use hello following command tooopen hello Hive console:</span></span>
   
        hive
3. <span data-ttu-id="920da-189">執行下列命令 tooshow hello 叢集中的 Hive 資料表的 hello:</span><span class="sxs-lookup"><span data-stu-id="920da-189">Run hello following command tooshow Hive tables in hello cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="920da-190">刪除邊緣節點</span><span class="sxs-lookup"><span data-stu-id="920da-190">Delete an edge node</span></span>
<span data-ttu-id="920da-191">您可以從 hello Azure 入口網站來刪除邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="920da-191">You can delete an edge node from hello Azure portal.</span></span>

<span data-ttu-id="920da-192">**tooaccess 邊緣節點**</span><span class="sxs-lookup"><span data-stu-id="920da-192">**tooaccess an edge node**</span></span>

1. <span data-ttu-id="920da-193">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="920da-193">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="920da-194">與邊緣節點開啟 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-194">Open hello HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="920da-195">按一下**應用程式**從 hello 叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="920da-195">Click **Applications** from hello cluster blade.</span></span> <span data-ttu-id="920da-196">您應該會看到邊緣節點清單。</span><span class="sxs-lookup"><span data-stu-id="920da-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="920da-197">以滑鼠右鍵按一下 hello 邊緣節點 toodelete，然後再按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="920da-197">Right-click hello edge node you want toodelete, and then click **Delete**.</span></span>
5. <span data-ttu-id="920da-198">按一下**是**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="920da-198">Click **Yes** tooconfirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="920da-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="920da-199">Next steps</span></span>
<span data-ttu-id="920da-200">在本文中，您已經學會如何 tooadd 邊緣節點和 tooaccess hello 邊緣節點的方式。</span><span class="sxs-lookup"><span data-stu-id="920da-200">In this article, you have learned how tooadd an edge node and how tooaccess hello edge node.</span></span> <span data-ttu-id="920da-201">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="920da-201">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="920da-202">[安裝的應用程式 HDInsight](hdinsight-apps-install-applications.md)： 了解如何 tooinstall HDInsight 應用程式 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how tooinstall an HDInsight application tooyour clusters.</span></span>
* <span data-ttu-id="920da-203">[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)： 了解如何 toodeploy 未發行的 HDInsight 應用程式 tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="920da-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how toodeploy an unpublished HDInsight application tooHDInsight.</span></span>
* <span data-ttu-id="920da-204">[發行 HDInsight 應用程式](hdinsight-apps-publish-applications.md)： 了解如何 toopublish 您自訂的 HDInsight 應用程式 tooAzure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="920da-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how toopublish your custom HDInsight applications tooAzure Marketplace.</span></span>
* <span data-ttu-id="920da-205">[MSDN： 安裝 HDInsight 應用程式](https://msdn.microsoft.com/library/mt706515.aspx)： 了解如何 toodefine HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="920da-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how toodefine HDInsight applications.</span></span>
* <span data-ttu-id="920da-206">[自訂使用指令碼動作以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)： 了解如何 toouse 指令碼動作 tooinstall 其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="920da-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how toouse Script Action tooinstall additional applications.</span></span>
* <span data-ttu-id="920da-207">[使用資源管理員範本 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)： 了解如何 toocall 資源管理員範本 toocreate HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="920da-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how toocall Resource Manager templates toocreate HDInsight clusters.</span></span>

