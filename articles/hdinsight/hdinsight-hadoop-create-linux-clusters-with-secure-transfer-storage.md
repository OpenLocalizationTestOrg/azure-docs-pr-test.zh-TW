---
title: "在 Azure HDInsight 中使用安全傳輸儲存體帳戶建立 Hadoop 叢集 | Microsoft Docs"
description: "了解如何使用已啟用安全傳輸的 Azure 儲存體帳戶建立 HDInsight 叢集。"
keywords: "hadoop 使用者入門,hadoop linux,hadoop 快速入門,安全傳輸,azure 儲存體帳戶"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 370b2f081930fe88527436a1a127309aed6681f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="ac5b5-104">在 Azure HDInsight 中使用安全傳輸儲存體帳戶建立 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="ac5b5-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="ac5b5-105">[需要安全傳輸](../storage/common/storage-require-secure-transfer.md)功能透過安全連線來強制對您帳戶的所有要求，以增強 Azure 儲存體帳戶的安全性。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-105">The [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances the security of your Azure Storage account by enforcing all requests to your account through a secure connection.</span></span> <span data-ttu-id="ac5b5-106">只有 HDInsight 叢集 3.6 版或更新版本支援這項功能和 wasbs 配置。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-106">This feature and the wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ac5b5-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="ac5b5-107">Prerequisites</span></span>
<span data-ttu-id="ac5b5-108">開始進行本教學課程之前，您必須具備：</span><span class="sxs-lookup"><span data-stu-id="ac5b5-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="ac5b5-109">**Azure 訂用帳戶**︰若要建立一個月的免費試用帳戶，請瀏覽至 [azure.microsoft.com/free](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-109">**Azure subscription**: To create a free one-month trial account, browse to [azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="ac5b5-110">**已啟用安全傳輸的 Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="ac5b5-111">如需相關指示，請參閱[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)和[需要安全傳輸](../storage/common/storage-require-secure-transfer.md)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-111">For the instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="ac5b5-112">**儲存體帳戶上的 Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-112">**A Blob container on the storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="ac5b5-113">建立叢集</span><span class="sxs-lookup"><span data-stu-id="ac5b5-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="ac5b5-114">在本節中，您會在 HDInsight 中使用 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)建立 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="ac5b5-115">這個範本位於 [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/) 中。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-115">The template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="ac5b5-116">進行本教學課程並不需要具備 Resource Manager 範本經驗。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="ac5b5-117">如需其他叢集建立方法及了解本教學課程中使用的屬性，請參閱 [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-117">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="ac5b5-118">按一下以下影像，在 Azure 入口網站中登入 Azure 並開啟 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-118">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="ac5b5-119">請依照指示建立具有下列規格的叢集：</span><span class="sxs-lookup"><span data-stu-id="ac5b5-119">Follow the instructions to create the cluster with the following specifications:</span></span> 

    - <span data-ttu-id="ac5b5-120">指定 HDInsight 3.6 版。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="ac5b5-121">預設版本為 3.5。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-121">The default version is 3.5.</span></span> <span data-ttu-id="ac5b5-122">需要 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="ac5b5-123">指定已啟用安全傳輸的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="ac5b5-124">使用儲存體帳戶的簡短名稱。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-124">Use short name for the storage account.</span></span>
    - <span data-ttu-id="ac5b5-125">必須事先建立儲存體帳戶和 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-125">Both the storage account and the blob container must be created beforehand.</span></span> 

    <span data-ttu-id="ac5b5-126">如需相關指示，請參閱[建立叢集](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-126">For the instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="ac5b5-127">如果您使用指令碼動作來提供自己的組態檔，您必須在下列設定中使用 wasbs：</span><span class="sxs-lookup"><span data-stu-id="ac5b5-127">If you use script action to provide your own configuration files, you must use wasbs in the following settings:</span></span>

- <span data-ttu-id="ac5b5-128">fs.defaultFS (core-site)</span><span class="sxs-lookup"><span data-stu-id="ac5b5-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="ac5b5-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="ac5b5-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="ac5b5-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="ac5b5-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="ac5b5-131">新增其他儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ac5b5-131">Add additional storage accounts</span></span>

<span data-ttu-id="ac5b5-132">有數個選項可新增其他已啟用安全傳輸的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="ac5b5-132">There are several options to add additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="ac5b5-133">在最後一節中修改 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-133">Modify the Azure Resource Manager template in the last section.</span></span>
- <span data-ttu-id="ac5b5-134">使用 [Azure 入口網站](https://portal.azure.com)建立叢集並指定連結的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-134">Create a cluster using the [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="ac5b5-135">使用指令碼動作，將其他已啟用安全傳輸的儲存體帳戶新增至現有的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-135">Use script action to add additional secure transfer enabled storage accounts to an existing HDInsight cluster.</span></span>  <span data-ttu-id="ac5b5-136">如需詳細資訊，請參閱[將其他儲存體帳戶新增至 HDInsight](hdinsight-hadoop-add-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-136">For more information, see [Add additional storage accounts to HDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac5b5-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac5b5-137">Next steps</span></span>
<span data-ttu-id="ac5b5-138">在本教學課程中，您已了解如何建立 HDInsight 叢集，並啟用儲存體帳戶的安全傳輸。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-138">In this tutorial, you have learned how to create an HDInsight cluster, and enable secure transfer to the storage accounts.</span></span>

<span data-ttu-id="ac5b5-139">若要深入了解如何使用 HDInsight 分析資料，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="ac5b5-139">To learn more about analyzing data with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="ac5b5-140">若要深入了解如何搭配 HDInsight 使用 Hive，包括如何從 Visual Studio 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 Hive][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-140">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="ac5b5-141">若要了解用來轉換資料的 Pig 語言，請參閱[搭配 HDInsight 使用 Pig][hdinsight-use-pig]。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-141">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="ac5b5-142">若要了解 MapReduce (一種撰寫程式以處理 Hadoop 資料的方式)，請參閱[搭配 HDInsight 使用 MapReduce][hdinsight-use-mapreduce]。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-142">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="ac5b5-143">若要了解如何使用適用於 Visual Studio 的 HDInsight 工具來分析 HDInsight 資料，請參閱 [開始使用 Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-143">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="ac5b5-144">若要進一步了解 HDInsight 如何儲存資料或如何將資料匯入 HDInsight 中，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="ac5b5-144">To learn more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span></span>

* <span data-ttu-id="ac5b5-145">如需有關 HDInsight 如何使用 Azure 儲存體的資訊，請參閱 [搭配 HDInsight 使用 Azure 儲存體](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="ac5b5-146">如需如何上傳資料到 HDInsight 的資訊，請參閱[將資料上傳到 HDInsight][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-146">For information on how to upload data to HDInsight, see [Upload data to HDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="ac5b5-147">若要深入了解如何建立或管理 HDInsight 叢集，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="ac5b5-147">To learn more about creating or managing an HDInsight cluster, see the following articles:</span></span>

* <span data-ttu-id="ac5b5-148">若要了解如何管理以 Linux 為基礎的 HDInsight 叢集，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-148">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="ac5b5-149">若要深入了解建立 HDInsight 叢集時可選取的選項，請參閱 [使用自訂選項在 Linux 上建立 HDInsight](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-149">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="ac5b5-150">如果您已熟悉 Linux 和 Hadoop，但想要知道在 HDInsight 上有關 Hadoop 的特定資訊，請參閱 [在 Linux 上使用 HDInsight](hdinsight-hadoop-linux-information.md)。</span><span class="sxs-lookup"><span data-stu-id="ac5b5-150">If you are familiar with Linux, and Hadoop, but want to know specifics about Hadoop on the HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="ac5b5-151">本文提供的資訊如下：</span><span class="sxs-lookup"><span data-stu-id="ac5b5-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="ac5b5-152">裝載於叢集上的服務 (例如 Ambari 和 WebHCat) URL</span><span class="sxs-lookup"><span data-stu-id="ac5b5-152">URLs for services hosted on the cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="ac5b5-153">Hadoop 檔案和範例在本機檔案系統上的位置</span><span class="sxs-lookup"><span data-stu-id="ac5b5-153">The location of Hadoop files and examples on the local file system</span></span>
  * <span data-ttu-id="ac5b5-154">Azure 儲存體 (WASB) (而非 HDFS) 做為預設資料儲存體的使用方式</span><span class="sxs-lookup"><span data-stu-id="ac5b5-154">The use of Azure Storage (WASB) instead of HDFS as the default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


