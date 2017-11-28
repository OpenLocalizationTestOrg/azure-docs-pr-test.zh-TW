---
title: "使用傳輸安全儲存體帳戶的 Azure HDInsight 叢集 aaaCreate Hadoop |Microsoft 文件"
description: "了解與安全傳輸 toocreate HDInsight 叢集如何啟用 Azure 儲存體帳戶。"
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
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="ed680-104">在 Azure HDInsight 中使用安全傳輸儲存體帳戶建立 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="ed680-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="ed680-105">hello[安全傳輸需要](../storage/common/storage-require-secure-transfer.md)功能增強 hello Azure 儲存體帳戶的安全性，方法是強制所有要求 tooyour 帳戶透過安全的連線。</span><span class="sxs-lookup"><span data-stu-id="ed680-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="ed680-106">HDInsight 叢集版本 3.6 版或更新版本才支援這個功能和 hello wasbs 配置。</span><span class="sxs-lookup"><span data-stu-id="ed680-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ed680-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="ed680-107">Prerequisites</span></span>
<span data-ttu-id="ed680-108">開始進行本教學課程之前，您必須具備：</span><span class="sxs-lookup"><span data-stu-id="ed680-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="ed680-109">**Azure 訂用帳戶**: toocreate 免費的一個月試用版帳戶，瀏覽過[azure.microsoft.com/free](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="ed680-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="ed680-110">**已啟用安全傳輸的 Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ed680-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="ed680-111">Hello 指示，請參閱[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)和[需要安全傳輸](../storage/common/storage-require-secure-transfer.md)。</span><span class="sxs-lookup"><span data-stu-id="ed680-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="ed680-112">**在 hello 儲存體帳戶 Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="ed680-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="ed680-113">建立叢集</span><span class="sxs-lookup"><span data-stu-id="ed680-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="ed680-114">在本節中，您會在 HDInsight 中使用 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)建立 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="ed680-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="ed680-115">hello 範本位於[Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/)。</span><span class="sxs-lookup"><span data-stu-id="ed680-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="ed680-116">進行本教學課程並不需要具備 Resource Manager 範本經驗。</span><span class="sxs-lookup"><span data-stu-id="ed680-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="ed680-117">適用於其他叢集建立方法，並了解本教學課程中使用的 hello 內容，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="ed680-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="ed680-118">按一下下列 tooAzure 中的映像 toosign 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ed680-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="ed680-119">請遵循 hello 指示 toocreate hello 叢集以 hello 下列規格：</span><span class="sxs-lookup"><span data-stu-id="ed680-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="ed680-120">指定 HDInsight 3.6 版。</span><span class="sxs-lookup"><span data-stu-id="ed680-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="ed680-121">hello 預設版本為 3.5。</span><span class="sxs-lookup"><span data-stu-id="ed680-121">hello default version is 3.5.</span></span> <span data-ttu-id="ed680-122">需要 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ed680-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="ed680-123">指定已啟用安全傳輸的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed680-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="ed680-124">使用 hello 儲存體帳戶的簡短名稱。</span><span class="sxs-lookup"><span data-stu-id="ed680-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="ed680-125">必須事先建立 hello 儲存體帳戶和 hello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="ed680-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="ed680-126">Hello 指示，請參閱[建立叢集](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。</span><span class="sxs-lookup"><span data-stu-id="ed680-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="ed680-127">如果您使用指令碼動作 tooprovide 您自己的組態檔，您必須使用 wasbs 在 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="ed680-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="ed680-128">fs.defaultFS (core-site)</span><span class="sxs-lookup"><span data-stu-id="ed680-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="ed680-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="ed680-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="ed680-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="ed680-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="ed680-131">新增其他儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ed680-131">Add additional storage accounts</span></span>

<span data-ttu-id="ed680-132">有數個選項 tooadd 額外的安全傳輸啟用儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="ed680-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="ed680-133">修改 hello 最後一節中的 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ed680-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="ed680-134">建立叢集使用 hello [Azure 入口網站](https://portal.azure.com)並指定連結的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed680-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="ed680-135">使用指令碼動作 tooadd 額外保護傳輸中啟用儲存體帳戶 tooan 現有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ed680-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="ed680-136">如需詳細資訊，請參閱[新增額外的儲存體帳戶 tooHDInsight](hdinsight-hadoop-add-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="ed680-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed680-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed680-137">Next steps</span></span>
<span data-ttu-id="ed680-138">在本教學課程中，您已經學會如何 toocreate 的 HDInsight 叢集，並啟用安全傳輸 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed680-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="ed680-139">toolearn 有關使用 HDInsight，分析資料的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="ed680-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="ed680-140">toolearn 更多有關搭配使用 Hive 與 HDInsight，包括如何 tooperform Hive 查詢從 Visual Studio，請參閱[使用 Hive 與 HDInsight][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="ed680-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="ed680-141">關於 Pig toolearn，使用語言 tootransform 資料，請參閱[與 HDInsight 搭配使用 Pig][hdinsight-use-pig]。</span><span class="sxs-lookup"><span data-stu-id="ed680-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="ed680-142">toolearn 有關 MapReduce，方式 toowrite 程式的處理資料的 Hadoop，請參閱[與 HDInsight 的使用 MapReduce][hdinsight-use-mapreduce]。</span><span class="sxs-lookup"><span data-stu-id="ed680-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="ed680-143">請參閱有關使用 hello HDInsight Tools for Visual Studio tooanalyze 資料在 HDInsight 上 toolearn[開始使用 Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ed680-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="ed680-144">深入了解 HDInsight 如何儲存資料的 toolearn 或如何 tooget 至 HDInsight 的資料，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="ed680-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="ed680-145">如需有關 HDInsight 如何使用 Azure 儲存體的資訊，請參閱 [搭配 HDInsight 使用 Azure 儲存體](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="ed680-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="ed680-146">如需詳細資訊 tooupload 資料 tooHDInsight，請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="ed680-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="ed680-147">toolearn 進一步了解建立或管理的 HDInsight 叢集，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="ed680-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="ed680-148">toolearn 關於管理您的 Linux 為基礎的 HDInsight 叢集，請參閱[使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="ed680-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="ed680-149">toolearn 進一步了解 hello 選項，您可以選取當建立 HDInsight 叢集，請參閱[建立使用自訂選項的 Linux 的 HDInsight](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="ed680-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="ed680-150">如果您熟悉 Linux 及 Hadoop，但是想 tooknow 特點 Hadoop hello HDInsight 上的時，請參閱[Linux 上使用 HDInsight](hdinsight-hadoop-linux-information.md)。</span><span class="sxs-lookup"><span data-stu-id="ed680-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="ed680-151">本文提供的資訊如下：</span><span class="sxs-lookup"><span data-stu-id="ed680-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="ed680-152">裝載在 hello 叢集上，例如 Ambari 和 WebHCat 服務的 Url</span><span class="sxs-lookup"><span data-stu-id="ed680-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="ed680-153">hello 位置的 Hadoop 檔案與 hello 本機檔案系統上的範例</span><span class="sxs-lookup"><span data-stu-id="ed680-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="ed680-154">hello 使用的 Azure 儲存體 (WASB) 而不是 HDFS 做 hello 預設資料存放區</span><span class="sxs-lookup"><span data-stu-id="ed680-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


