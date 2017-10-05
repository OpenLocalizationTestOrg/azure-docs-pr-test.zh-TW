---
title: "使用 Azure CLI 管理 Hadoop 叢集 - Azure HDInsight| Microsoft Docs"
description: "了解如何使用 Azure 命令列介面來管理 Azure HDInsight 中的 Hadoop 叢集。 Azure CLI 適用於 Windows、Mac 和 Linux。"
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
ms.openlocfilehash: 0ee9f2f28978b207dcaf8f77950bd82a897d3fd1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="8b40e-104">使用 Azure CLI 管理 HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="8b40e-104">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="8b40e-105">了解如何使用 [Azure 命令列介面](../cli-install-nodejs.md)來管理 Azure HDInsight 中的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="8b40e-105">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="8b40e-106">Azure CLI 是在 Node.js 中實作。</span><span class="sxs-lookup"><span data-stu-id="8b40e-106">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="8b40e-107">此工具可在任何支援 Node.js 的平台上使用，包括 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="8b40e-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="8b40e-108">本文只涵蓋搭配 HDInsight 使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="8b40e-108">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="8b40e-109">如需如何使用 Azure CLI 的一般指南，請參閱[安裝及設定 Azure CLI][azure-command-line-tools]。</span><span class="sxs-lookup"><span data-stu-id="8b40e-109">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="8b40e-110">先決條件</span><span class="sxs-lookup"><span data-stu-id="8b40e-110">Prerequisites</span></span>
<span data-ttu-id="8b40e-111">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="8b40e-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="8b40e-112">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8b40e-112">**An Azure subscription**.</span></span> <span data-ttu-id="8b40e-113">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="8b40e-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8b40e-114">**Azure CLI** - 請參閱[安裝及設定 Azure CLI](../cli-install-nodejs.md) 以取得安裝和設定資訊。</span><span class="sxs-lookup"><span data-stu-id="8b40e-114">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="8b40e-115">**連線到 Azure**，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="8b40e-115">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="8b40e-116">如需使用公司或學校帳戶驗證的詳細資訊，請參閱[從 Azure CLI 連線至 Azure 訂用帳戶](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="8b40e-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="8b40e-117">使用下列命令來**切換至 Azure 資源管理員模式**：</span><span class="sxs-lookup"><span data-stu-id="8b40e-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="8b40e-118">若要取得說明，請使用 **-h** 參數。</span><span class="sxs-lookup"><span data-stu-id="8b40e-118">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="8b40e-119">例如：</span><span class="sxs-lookup"><span data-stu-id="8b40e-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-the-cli"></a><span data-ttu-id="8b40e-120">使用 CLI 建立叢集</span><span class="sxs-lookup"><span data-stu-id="8b40e-120">Create clusters with the CLI</span></span>
<span data-ttu-id="8b40e-121">請參閱[使用 Azure CLI 建立 HDInsight 中的叢集](hdinsight-hadoop-create-linux-clusters-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="8b40e-121">See [Create clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="8b40e-122">列出和顯示叢集詳細資料</span><span class="sxs-lookup"><span data-stu-id="8b40e-122">List and show cluster details</span></span>
<span data-ttu-id="8b40e-123">使用下列命令，以列出並顯示叢集詳細資料：</span><span class="sxs-lookup"><span data-stu-id="8b40e-123">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="8b40e-124">![叢集清單的命令列檢視][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="8b40e-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="8b40e-125">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="8b40e-125">Delete clusters</span></span>
<span data-ttu-id="8b40e-126">使用下列命令來刪除叢集：</span><span class="sxs-lookup"><span data-stu-id="8b40e-126">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="8b40e-127">您也可以刪除包含叢集的資源群組來刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="8b40e-127">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="8b40e-128">請注意，這將會刪除群組中的所有資源 (包括預設儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="8b40e-128">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="8b40e-129">調整叢集</span><span class="sxs-lookup"><span data-stu-id="8b40e-129">Scale clusters</span></span>
<span data-ttu-id="8b40e-130">若要變更 Hadoop 叢集大小：</span><span class="sxs-lookup"><span data-stu-id="8b40e-130">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="8b40e-131">啟用/停用叢集 HTTP 存取</span><span class="sxs-lookup"><span data-stu-id="8b40e-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="8b40e-132">啟用/停用叢集 RDP 存取</span><span class="sxs-lookup"><span data-stu-id="8b40e-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="8b40e-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b40e-133">Next steps</span></span>
<span data-ttu-id="8b40e-134">本文中，您學到如何執行不同的 HDInsight 叢集管理工作。</span><span class="sxs-lookup"><span data-stu-id="8b40e-134">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="8b40e-135">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="8b40e-135">To learn more, see the following articles:</span></span>

* <span data-ttu-id="8b40e-136">[使用 Azure 入口網站管理 HDInsight][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="8b40e-136">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="8b40e-137">[使用 Azure PowerShell 管理 HDInsight][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="8b40e-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="8b40e-138">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="8b40e-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="8b40e-139">[如何使用 Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="8b40e-139">[How to use the Azure CLI][azure-command-line-tools]</span></span>

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
