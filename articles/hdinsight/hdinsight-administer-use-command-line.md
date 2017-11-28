---
title: "使用 Azure CLI-Azure HDInsight aaaManage Hadoop 叢集 |Microsoft 文件"
description: "了解在 Azure HDInsight toouse hello Azure 命令列介面 toomanage Hadoop 叢集的方式。 hello Azure CLI 適用於 Windows、 Mac 和 Linux。"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="731b7-104">管理中使用 Azure CLI hello HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="731b7-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="731b7-105">深入了解如何 toouse hello [Azure 命令列介面](../cli-install-nodejs.md)toomanage Hadoop Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="731b7-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="731b7-106">Node.js 被實作 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="731b7-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="731b7-107">此工具可在任何支援 Node.js 的平台上使用，包括 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="731b7-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="731b7-108">本文涵蓋只使用 HDInsight 中的 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="731b7-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="731b7-109">有關的一般指南 toouse Azure CLI，請參閱[安裝及設定 Azure CLI][azure-command-line-tools]。</span><span class="sxs-lookup"><span data-stu-id="731b7-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="731b7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="731b7-110">Prerequisites</span></span>
<span data-ttu-id="731b7-111">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="731b7-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="731b7-112">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="731b7-112">**An Azure subscription**.</span></span> <span data-ttu-id="731b7-113">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="731b7-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="731b7-114">**Azure CLI** -請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)如需安裝和組態資訊。</span><span class="sxs-lookup"><span data-stu-id="731b7-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="731b7-115">**連接 tooAzure**，並使用下列命令 hello:</span><span class="sxs-lookup"><span data-stu-id="731b7-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="731b7-116">如需有關如何使用工作或學校帳戶驗證的詳細資訊，請參閱[tooan Azure 訂用帳戶連線從 hello Azure CLI](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="731b7-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="731b7-117">**交換器 toohello Azure Resource Manager 模式**，並使用下列命令 hello:</span><span class="sxs-lookup"><span data-stu-id="731b7-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="731b7-118">tooget 的說明，請使用 hello **-h**切換。</span><span class="sxs-lookup"><span data-stu-id="731b7-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="731b7-119">例如：</span><span class="sxs-lookup"><span data-stu-id="731b7-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="731b7-120">以 hello CLI 建立叢集</span><span class="sxs-lookup"><span data-stu-id="731b7-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="731b7-121">請參閱[中使用 HDInsight 建立叢集 hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="731b7-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="731b7-122">列出和顯示叢集詳細資料</span><span class="sxs-lookup"><span data-stu-id="731b7-122">List and show cluster details</span></span>
<span data-ttu-id="731b7-123">使用下列命令 toolist hello，並顯示叢集詳細資料：</span><span class="sxs-lookup"><span data-stu-id="731b7-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="731b7-124">![叢集清單的命令列檢視][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="731b7-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="731b7-125">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="731b7-125">Delete clusters</span></span>
<span data-ttu-id="731b7-126">使用下列命令 toodelete 叢集中的 hello:</span><span class="sxs-lookup"><span data-stu-id="731b7-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="731b7-127">您也可以藉由刪除 hello 資源群組含有 hello 叢集刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="731b7-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="731b7-128">請注意，這將刪除 hello 群組包括 hello 預設儲存體帳戶中的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="731b7-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="731b7-129">調整叢集</span><span class="sxs-lookup"><span data-stu-id="731b7-129">Scale clusters</span></span>
<span data-ttu-id="731b7-130">toochange hello Hadoop 叢集大小：</span><span class="sxs-lookup"><span data-stu-id="731b7-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="731b7-131">啟用/停用叢集 HTTP 存取</span><span class="sxs-lookup"><span data-stu-id="731b7-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="731b7-132">啟用/停用叢集 RDP 存取</span><span class="sxs-lookup"><span data-stu-id="731b7-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="731b7-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="731b7-133">Next steps</span></span>
<span data-ttu-id="731b7-134">在本文中，您已經學會如何 tooperform 不同 HDInsight 叢集系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="731b7-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="731b7-135">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="731b7-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="731b7-136">[使用 hello Azure 入口網站來管理 HDInsight][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="731b7-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="731b7-137">[使用 Azure PowerShell 管理 HDInsight][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="731b7-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="731b7-138">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="731b7-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="731b7-139">[如何 toouse hello Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="731b7-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "列出和顯示叢集"
