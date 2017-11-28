---
title: "在 HDInsight 中使用 aaaManage Windows 為基礎的 Hadoop 叢集 hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 tooadminister HDInsight 服務。 建立 HDInsight 叢集、 開啟 hello 互動式 JavaScript 主控台與開啟的 hello Hadoop 命令主控台。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a><span data-ttu-id="f2bd9-104">透過 hello Azure 入口網站來管理 HDInsight 中的 Windows 架構的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="f2bd9-104">Manage Windows-based Hadoop clusters in HDInsight by using hello Azure portal</span></span>

<span data-ttu-id="f2bd9-105">使用 hello [Azure 入口網站][azure-portal]，您可以在 Azure HDInsight 中建立 Windows 架構的 Hadoop 叢集變更 Hadoop 使用者的密碼，以及啟用遠端桌面通訊協定 (RDP) 讓您能夠存取 hello Hadoophello 叢集上的命令主控台。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-105">Using hello [Azure portal][azure-portal], you can create Windows-based Hadoop clusters in Azure HDInsight, change Hadoop user password, and enable Remote Desktop Protocol (RDP) so you can access hello Hadoop command console on hello cluster.</span></span>

<span data-ttu-id="f2bd9-106">本文章中的 hello 資訊僅適用於 tooWindow 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-106">hello information in this article only applies tooWindow-based HDInsight clusters.</span></span> <span data-ttu-id="f2bd9-107">如需管理以 Linux 為基礎的叢集資訊，請參閱[HDInsight 中使用的管理 Hadoop 叢集 hello Azure 入口網站](hdinsight-administer-use-portal-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-107">For information on managing Linux-based clusters, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-portal-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2bd9-108">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f2bd9-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f2bd9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f2bd9-110">Prerequisites</span></span>

<span data-ttu-id="f2bd9-111">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="f2bd9-112">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-112">**An Azure subscription**.</span></span> <span data-ttu-id="f2bd9-113">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="f2bd9-114">**Azure 儲存體帳戶**-HDInsight 叢集會為 hello 預設檔案系統中使用 Azure Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-114">**Azure Storage account** - An HDInsight cluster uses an Azure Blob storage container as hello default file system.</span></span> <span data-ttu-id="f2bd9-115">如需 Azure Blob 儲存體如何提供順暢 HDInsight 叢集使用體驗的詳細資訊，請參閱 [搭配使用 Azure Blob 儲存體與 HDInsight](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-115">For more information about how Azure Blob storage provides a seamless experience with HDInsight clusters, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="f2bd9-116">如需有關建立 Azure 儲存體帳戶的詳細資訊，請參閱[如何 tooCreate 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-116">For details on creating an Azure Storage account, see [How tooCreate a Storage Account](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="open-hello-portal"></a><span data-ttu-id="f2bd9-117">開啟 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="f2bd9-117">Open hello Portal</span></span>
1. <span data-ttu-id="f2bd9-118">登入太[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-118">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f2bd9-119">開啟 hello 入口網站之後，您可以：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-119">After you open hello portal, you can:</span></span>

   * <span data-ttu-id="f2bd9-120">按一下**新增**從 hello 左側的功能表 toocreate 新叢集：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-120">Click **New** from hello left menu toocreate a new cluster:</span></span>

       ![新的 HDInsight 叢集按鈕](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * <span data-ttu-id="f2bd9-122">按一下**HDInsight 叢集**hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-122">Click **HDInsight Clusters** from hello left menu.</span></span>

       ![Azure 入口網站 HDInsight 叢集按鈕](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     <span data-ttu-id="f2bd9-124">如果**HDInsight**未出現在 hello 左側功能表中，按一下**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-124">If **HDInsight** doesn't appear in hello left menu, click **Browse**.</span></span>

     ![Azure 入口網站瀏覽叢集按鈕](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a><span data-ttu-id="f2bd9-126">建立叢集</span><span class="sxs-lookup"><span data-stu-id="f2bd9-126">Create clusters</span></span>
<span data-ttu-id="f2bd9-127">Hello 建立指示使用 hello 入口網站，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-127">For hello creation instructions using hello Portal, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="f2bd9-128">HDInsight 可以與很多 Hadoop 元件搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-128">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="f2bd9-129">Hello 驗證以及支援 hello 元件清單，請參閱[的 Hadoop 版本是在 Azure HDInsight](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-129">For hello list of hello components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="f2bd9-130">您可以自訂 HDInsight 使用其中一種 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-130">You can customize HDInsight by using one of hello following options:</span></span>

* <span data-ttu-id="f2bd9-131">使用指令碼動作 toorun 自訂指令碼，可以自訂叢集 tooeither 變更叢集設定，或安裝自訂元件，例如 Giraph 或 Solr。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-131">Use Script Action toorun custom scripts that can customize a cluster tooeither change cluster configuration or install custom components such as Giraph or Solr.</span></span> <span data-ttu-id="f2bd9-132">如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-132">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span>
* <span data-ttu-id="f2bd9-133">在叢集建立期間使用 hello HDInsight.NET SDK 或 Azure PowerShell 中的 hello 叢集自訂參數。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-133">Use hello cluster customization parameters in hello HDInsight .NET SDK or Azure PowerShell during cluster creation.</span></span> <span data-ttu-id="f2bd9-134">這些組態變更再透過 hello 存留期的 hello 叢集保留，並不會受到 Azure 平台會定期執行維護的叢集節點 reimages。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-134">These configuration changes are then preserved through hello lifetime of hello cluster and are not affected by cluster node reimages that Azure platform periodically performs for maintenance.</span></span> <span data-ttu-id="f2bd9-135">如需有關使用 hello 叢集自訂參數的詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-135">For more information on using hello cluster customization parameters, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="f2bd9-136">某些原生 Java 元件，例如砲象兵和 Cascading，可以當做 JAR 檔案 hello 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-136">Some native Java components, like Mahout and Cascading, can be run on hello cluster as JAR files.</span></span> <span data-ttu-id="f2bd9-137">這些 JAR 檔案可以是分散式的 tooAzure Blob 儲存體，並透過 Hadoop 工作提交機制提交 tooHDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-137">These JAR files can be distributed tooAzure Blob storage, and submitted tooHDInsight clusters through Hadoop job submission mechanisms.</span></span> <span data-ttu-id="f2bd9-138">如需詳細資訊，請參閱 [以程式設計方式提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-138">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

  > [!NOTE]
  > <span data-ttu-id="f2bd9-139">如果您有部署 JAR 檔案 tooHDInsight 叢集的問題，或呼叫 JAR 檔案，在 HDInsight 叢集，請連絡[Microsoft 支援服務](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-139">If you have issues deploying JAR files tooHDInsight clusters or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
  >
  > <span data-ttu-id="f2bd9-140">Cascading 不受 HDInsight 支援，而且不符合「Microsoft 支援」的資格。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-140">Cascading is not supported by HDInsight, and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="f2bd9-141">支援的元件清單中，請參閱[hello 叢集版本 HDInsight 所提供的新](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-141">For lists of supported components, see [What's new in hello cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
  >
  >

<span data-ttu-id="f2bd9-142">不支援使用遠端桌面連線的 hello 叢集上的自訂軟體安裝。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-142">Installation of custom software on hello cluster by using Remote Desktop Connection is not supported.</span></span> <span data-ttu-id="f2bd9-143">您應該避免儲存 hello hello 前端節點之後，磁碟機上的任何檔案因為它們將會遺失如果您需要 toore-建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-143">You should avoid storing any files on hello drives of hello head node, as they will be lost if you need toore-create hello clusters.</span></span> <span data-ttu-id="f2bd9-144">建議您將檔案儲存至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-144">We recommend storing files on Azure Blob storage.</span></span> <span data-ttu-id="f2bd9-145">Blob 儲存體是持續性的。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-145">Blob storage is persistent.</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="f2bd9-146">列出和顯示叢集</span><span class="sxs-lookup"><span data-stu-id="f2bd9-146">List and show clusters</span></span>
1. <span data-ttu-id="f2bd9-147">登入太[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-147">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f2bd9-148">按一下**HDInsight 叢集**hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-148">Click **HDInsight Clusters** from hello left menu.</span></span>
3. <span data-ttu-id="f2bd9-149">按一下 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-149">Click hello cluster name.</span></span> <span data-ttu-id="f2bd9-150">如果 hello 叢集清單很長，您可以使用篩選器上 hello hello 頁面的頂端。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-150">If hello cluster list is long, you can use filter on hello top of hello page.</span></span>
4. <span data-ttu-id="f2bd9-151">按兩下叢集 hello 清單 tooshow hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-151">Double-click a cluster from hello list tooshow hello details.</span></span>

    <span data-ttu-id="f2bd9-152">**功能表和基本功能**：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-152">**Menu and essentials**:</span></span>

    ![Azure portal HDInsight cluster essentials](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * <span data-ttu-id="f2bd9-154">toocustomize hello 功能表上，hello 功能表上按一下滑鼠右鍵，然後按一下**自訂**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-154">toocustomize hello menu, right-click anywhere on hello menu, and then click **Customize**.</span></span>
   * <span data-ttu-id="f2bd9-155">**設定**和**所有設定**： 顯示 hello**設定**刀鋒視窗中的，可讓您 tooaccess hello 叢集組態的詳細資訊 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-155">**Settings** and **All Settings**: Displays hello **Settings** blade for hello cluster, which allows you tooaccess detailed configuration information for hello cluster.</span></span>
   * <span data-ttu-id="f2bd9-156">**儀表板**，**叢集儀表板**和**URL： 這些是所有方法 tooaccess hello 叢集儀表板，也就是 Ambari Web linux 叢集。-**安全殼層 * *: 顯示 hello 指示 tooconnect toohello 叢集使用安全殼層 (SSH) 連線。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-156">**Dashboard**, **Cluster Dashboard** and **URL: These are all ways tooaccess hello cluster dashboard, which is Ambari Web for Linux-based clusters. -**Secure Shell**: Shows hello instructions tooconnect toohello cluster using Secure Shell (SSH) connection.</span></span>
   * <span data-ttu-id="f2bd9-157">**調整叢集**： 可讓您對此叢集的背景工作節點 toochange hello 數。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-157">**Scale Cluster**: Allows you toochange hello number of worker nodes for this cluster.</span></span>
   * <span data-ttu-id="f2bd9-158">**刪除**： 刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-158">**Delete**: Deletes hello cluster.</span></span>
   * <span data-ttu-id="f2bd9-159">**快速啟動**：顯示可協助您開始使用 HDInsight 的資訊。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-159">**Quickstart**: Displays information that will help you get started using HDInsight.</span></span>
   * <span data-ttu-id="f2bd9-160">* * 使用者： 可讓您 tooset 權限*入口網站管理*此叢集的其他使用者 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-160">**Users: Allows you tooset permissions for *portal management* of this cluster for other users on your Azure subscription.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="f2bd9-161">這*只*影響 hello Azure 入口網站中的存取和權限 toothis 叢集，以及誰可以連線 tooor 送出工作 toohello HDInsight 叢集上沒有作用。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-161">This *only* affects access and permissions toothis cluster in hello Azure portal, and has no effect on who can connect tooor submit jobs toohello HDInsight cluster.</span></span>
     >
     >
   * <span data-ttu-id="f2bd9-162">**標記**： 標記可讓您 tooset 索引鍵/值組 toodefine 自訂您的雲端服務的分類。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-162">**Tags**: Tags allow you tooset key/value pairs toodefine a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="f2bd9-163">例如，您可建立名為 **project**的索引鍵，然後使用與特定專案相關聯之所有服務的通用值。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-163">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
   * <span data-ttu-id="f2bd9-164">**Ambari 檢視**： 連結 tooAmbari Web。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-164">**Ambari Views**: Links tooAmbari Web.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="f2bd9-165">toomanage hello 服務提供 hello HDInsight 叢集，您必須使用 Ambari Web 或 hello Ambari REST API。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-165">toomanage hello services provided by hello HDInsight cluster, you must use Ambari Web or hello Ambari REST API.</span></span> <span data-ttu-id="f2bd9-166">如需使用 Ambari 的詳細資訊，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-166">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
     >
     >

     <span data-ttu-id="f2bd9-167">**使用量**：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-167">**Usage**:</span></span>

     ![Azure 入口網站 HDInsight 叢集使用量](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. <span data-ttu-id="f2bd9-169">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-169">Click **Settings**.</span></span>

    ![Azure 入口網站 HDInsight 叢集使用量](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * <span data-ttu-id="f2bd9-171">**屬性**： 檢視 hello 叢集內容。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-171">**Properties**: View hello cluster properties.</span></span>
   * <span data-ttu-id="f2bd9-172">**叢集 AAD 身分識別**：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-172">**Cluster AAD Identity**:</span></span>
   * <span data-ttu-id="f2bd9-173">**Azure 儲存體金鑰**： 檢視 hello 預設儲存體帳戶和它的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-173">**Azure Storage Keys**: View hello default storage account and its key.</span></span> <span data-ttu-id="f2bd9-174">hello 叢集建立程序期間設定 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-174">hello storage account is configuration during hello cluster creation process.</span></span>
   * <span data-ttu-id="f2bd9-175">**叢集登入**: hello 叢集 HTTP 使用者名稱和密碼變更。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-175">**Cluster Login**: Change hello cluster HTTP user name and password.</span></span>
   * <span data-ttu-id="f2bd9-176">**外部中繼存放區**： 檢視 hello Hive 和 Oozie 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-176">**External Metastores**: View hello Hive and Oozie metastores.</span></span> <span data-ttu-id="f2bd9-177">只能在 hello 叢集建立程序期間設定 hello 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-177">hello metastores can only be configured during hello cluster creation process.</span></span>
   * <span data-ttu-id="f2bd9-178">**調整叢集**： 增減 hello 叢集背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-178">**Scale Cluster**: Increase and decrease hello number of cluster worker nodes.</span></span>
   * <span data-ttu-id="f2bd9-179">**遠端桌面**： 啟用和停用遠端桌面 (RDP) 存取和設定 hello RDP 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-179">**Remote Desktop**: Enable and disable remote desktop (RDP) access, and configure hello RDP username.</span></span>  <span data-ttu-id="f2bd9-180">hello RDP 使用者名稱必須不同於 hello HTTP 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-180">hello RDP user name must be different from hello HTTP user name.</span></span>
   * <span data-ttu-id="f2bd9-181">**記錄可查夥伴**：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-181">**Partner of Record**:</span></span>

     > [!NOTE]
     > <span data-ttu-id="f2bd9-182">這是可用設定的泛型清單，並不會針對所有叢集類型顯示所有的可用設定。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-182">This is a generic list of available settings; not all of them will be present for all cluster types.</span></span>
     >
     >
6. <span data-ttu-id="f2bd9-183">按一下 [屬性] ：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-183">Click **Properties**:</span></span>

    <span data-ttu-id="f2bd9-184">hello 屬性區段會列出 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-184">hello properties section lists hello following:</span></span>

   * <span data-ttu-id="f2bd9-185">**主機名稱**：叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="f2bd9-186">**叢集 URL**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-186">**Cluster URL**.</span></span>
   * <span data-ttu-id="f2bd9-187">**狀態**：包括Aborted、Accepted、ClusterStorageProvisioned、AzureVMConfiguration、HDInsightConfiguration、Operational、Running、Error、Deleting、Deleted、Timedout、DeleteQueued、DeleteTimedout、DeleteError、PatchQueued、CertRolloverQueued、ResizeQueued、ClusterCustomization</span><span class="sxs-lookup"><span data-stu-id="f2bd9-187">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="f2bd9-188">**區域**：Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-188">**Region**: Azure location.</span></span> <span data-ttu-id="f2bd9-189">如需支援的 Azure 位置的清單，請參閱 hello**區域**下拉式清單方塊上的[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-189">For a list of supported Azure locations, see hello **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="f2bd9-190">**資料已建立**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-190">**Data created**.</span></span>
   * <span data-ttu-id="f2bd9-191">**作業系統**：**Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-191">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="f2bd9-192">**類型**：Hadoop、HBase、Storm、Spark。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-192">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="f2bd9-193">**版本**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-193">**Version**.</span></span> <span data-ttu-id="f2bd9-194">請參閱 [HDInsight 版本](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="f2bd9-194">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="f2bd9-195">**訂用帳戶**︰訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-195">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="f2bd9-196">**訂用帳戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-196">**Subscription ID**.</span></span>
   * <span data-ttu-id="f2bd9-197">**主要資料來源**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-197">**Primary data source**.</span></span> <span data-ttu-id="f2bd9-198">hello Azure Blob 儲存體帳戶做為 hello 預設 Hadoop 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-198">hello Azure Blob storage account used as hello default Hadoop file system.</span></span>
   * <span data-ttu-id="f2bd9-199">**背景工作節點定價層**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-199">**Worker nodes pricing tier**.</span></span>
   * <span data-ttu-id="f2bd9-200">**前端節點定價層**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-200">**Head node pricing tier**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="f2bd9-201">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="f2bd9-201">Delete clusters</span></span>
<span data-ttu-id="f2bd9-202">刪除叢集時，不會刪除 hello 預設儲存體帳戶或任何連結儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-202">Delete a cluster will not delete hello default storage account or any linked storage accounts.</span></span> <span data-ttu-id="f2bd9-203">您可以使用，以重新建立 hello 叢集 hello 相同的儲存體帳戶和 hello 相同中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-203">You can re-create hello cluster by using hello same storage accounts and hello same metastores.</span></span>

1. <span data-ttu-id="f2bd9-204">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-204">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f2bd9-205">按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-205">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="f2bd9-206">按一下**刪除**從 hello 上方功能表中，然後再遵循 hello 的指示。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-206">Click **Delete** from hello top menu, and then follow hello instructions.</span></span>

<span data-ttu-id="f2bd9-207">另請參閱 [暫停/關閉叢集](#pauseshut-down-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-207">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="f2bd9-208">調整叢集</span><span class="sxs-lookup"><span data-stu-id="f2bd9-208">Scale clusters</span></span>
<span data-ttu-id="f2bd9-209">hello 叢集擴充功能可讓您在 Azure HDInsight 中執行而不需要 toore 叢集所用的背景工作節點 toochange hello 數-建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-209">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f2bd9-210">只支援使用 HDInsight 3.1.3 版或更高版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-210">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="f2bd9-211">如果您不確定您的叢集 hello 版本，您可以檢查 hello 屬性頁面。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-211">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="f2bd9-212">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-212">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="f2bd9-213">hello 變更造成的影響 hello 支援 HDInsight 叢集的每種類型的資料節點數目：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-213">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="f2bd9-214">Hadoop</span><span class="sxs-lookup"><span data-stu-id="f2bd9-214">Hadoop</span></span>

    <span data-ttu-id="f2bd9-215">您可以順暢地增加 hello Hadoop 叢集中執行而不會影響任何暫止或執行工作的背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-215">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="f2bd9-216">Hello 作業正在進行時，也可以提交新的作業。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-216">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="f2bd9-217">使 hello 叢集一律會保持在運作狀態，是依正常程序處理中縮放作業失敗。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-217">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="f2bd9-218">當在 Hadoop 叢集縮小藉由減少 hello 資料節點數時，部分 hello hello 叢集中的服務會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-218">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="f2bd9-219">這會導致所有執行和暫止的工作 toofail hello hello 調整大小作業完成時。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-219">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="f2bd9-220">您可以不過，再重新送出 hello 工作一旦 hello 作業已完成。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-220">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="f2bd9-221">HBase</span><span class="sxs-lookup"><span data-stu-id="f2bd9-221">HBase</span></span>

    <span data-ttu-id="f2bd9-222">順暢地，您可以新增或移除節點 tooyour HBase 叢集正在執行時。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-222">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="f2bd9-223">完成 hello 調整大小作業的幾分鐘內自動平衡地區的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-223">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="f2bd9-224">不過，您就可以手動平衡 hello 地區的伺服器登入 hello 叢集前端節點的叢集和執行 hello 的命令提示字元視窗中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-224">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="f2bd9-225">如需有關使用 hello HBase 殼層的詳細資訊，請參閱]</span><span class="sxs-lookup"><span data-stu-id="f2bd9-225">For more information on using hello HBase shell, see []</span></span>
* <span data-ttu-id="f2bd9-226">Storm</span><span class="sxs-lookup"><span data-stu-id="f2bd9-226">Storm</span></span>

    <span data-ttu-id="f2bd9-227">順暢地，您可以新增或移除在執行時的資料節點 tooyour Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-227">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="f2bd9-228">但是 hello 調整大小作業順利完成之後, 您將需要 toorebalance hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-228">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="f2bd9-229">您可以使用兩種方式來完成重新平衡作業：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-229">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="f2bd9-230">Storm Web UI</span><span class="sxs-lookup"><span data-stu-id="f2bd9-230">Storm web UI</span></span>
  * <span data-ttu-id="f2bd9-231">命令列介面 (CLI) 工具</span><span class="sxs-lookup"><span data-stu-id="f2bd9-231">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="f2bd9-232">請參閱 toohello [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-232">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="f2bd9-233">hello Storm web UI 是在 hello HDInsight 叢集上使用：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-233">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![hdinsight storm scale rebalance](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="f2bd9-235">以下是範例如何 toouse hello CLI 命令 toorebalance hello Storm 拓撲：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-235">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="f2bd9-236">**tooscale 叢集**</span><span class="sxs-lookup"><span data-stu-id="f2bd9-236">**tooscale clusters**</span></span>

1. <span data-ttu-id="f2bd9-237">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-237">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f2bd9-238">按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-238">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="f2bd9-239">按一下**設定**從 hello 最上層功能表，然後再按一下**延展叢集**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-239">Click **Settings** from hello top menu, and then click **Scale Cluster**.</span></span>
4. <span data-ttu-id="f2bd9-240">輸入 **背景工作節點的數目**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-240">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="f2bd9-241">hello hello 叢集節點數目限制會因 Azure 訂用帳戶而異。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-241">hello limit on hello number of cluster node varies among Azure subscriptions.</span></span> <span data-ttu-id="f2bd9-242">您可以連絡帳務支援 tooincrease hello 限制。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-242">You can contact billing support tooincrease hello limit.</span></span>  <span data-ttu-id="f2bd9-243">hello 成本資訊將會反映您所做的節點 toohello 數目的 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-243">hello cost information will reflect hello changes you have made toohello number of nodes.</span></span>

    ![HDInsight Hadoop HBase Storm Spark scale](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="f2bd9-245">暫停/關閉叢集</span><span class="sxs-lookup"><span data-stu-id="f2bd9-245">Pause/shut down clusters</span></span>
<span data-ttu-id="f2bd9-246">大部分 Hadoop 工作是只會偶爾執行的批次工作。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-246">Most of Hadoop jobs are batch jobs that are only ran occasionally.</span></span> <span data-ttu-id="f2bd9-247">對於大多數的 Hadoop 叢集有長時間的過 hello 叢集不正進行處理。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-247">For most Hadoop clusters, there are large periods of time that hello cluster is not being used for processing.</span></span> <span data-ttu-id="f2bd9-248">利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-248">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="f2bd9-249">您也需支付 HDInsight 叢集的費用 (即使未使用)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-249">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="f2bd9-250">由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-250">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span>

<span data-ttu-id="f2bd9-251">有許多方法，您可以程式設計 hello 程序：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-251">There are many ways you can program hello process:</span></span>

* <span data-ttu-id="f2bd9-252">使用 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-252">User Azure Data Factory.</span></span> <span data-ttu-id="f2bd9-253">請參閱 [Azure HDInsight 連結服務](../data-factory/data-factory-compute-linked-services.md)和[使用 Azure Data Factory 進行轉換和分析](../data-factory/data-factory-data-transformation-activities.md)，以取得隨選和自行定義的 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-253">See [Azure HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md) and [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) for on-demand and self-defined HDInsight linked services.</span></span>
* <span data-ttu-id="f2bd9-254">使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-254">Use Azure PowerShell.</span></span>  <span data-ttu-id="f2bd9-255">請參閱 [分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-255">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="f2bd9-256">使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-256">Use Azure CLI.</span></span> <span data-ttu-id="f2bd9-257">請參閱 [使用 Azure CLI 管理 HDInsight 叢集](hdinsight-administer-use-command-line.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-257">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="f2bd9-258">使用 HDInsight .NET SDK。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-258">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="f2bd9-259">請參閱 [提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-259">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="f2bd9-260">Hello 定價資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-260">For hello pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="f2bd9-261">請參閱 toodelete hello 入口網站中，從叢集[刪除叢集](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="f2bd9-261">toodelete a cluster from hello Portal, see [Delete clusters](#delete-clusters)</span></span>

## <a name="change-cluster-username"></a><span data-ttu-id="f2bd9-262">變更叢集使用者名稱</span><span class="sxs-lookup"><span data-stu-id="f2bd9-262">Change cluster username</span></span>
<span data-ttu-id="f2bd9-263">HDInsight 叢集可以有兩個使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-263">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="f2bd9-264">hello 建立程序期間建立的 hello HDInsight 叢集的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-264">hello HDInsight cluster user account is created during hello creation process.</span></span> <span data-ttu-id="f2bd9-265">您也可以建立存取透過 RDP hello 叢集的 RDP 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-265">You can also create an RDP user account for accessing hello cluster via RDP.</span></span> <span data-ttu-id="f2bd9-266">請參閱 [啟用遠端桌面](#connect-to-hdinsight-clusters-by-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-266">See [Enable remote desktop](#connect-to-hdinsight-clusters-by-using-rdp).</span></span>

<span data-ttu-id="f2bd9-267">**toochange hello HDInsight 叢集使用者名稱和密碼**</span><span class="sxs-lookup"><span data-stu-id="f2bd9-267">**toochange hello HDInsight cluster user name and password**</span></span>

1. <span data-ttu-id="f2bd9-268">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-268">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f2bd9-269">按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-269">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="f2bd9-270">按一下**設定**從 hello 最上層功能表，然後再按一下**叢集登入**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-270">Click **Settings** from hello top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="f2bd9-271">如果**叢集登入**已啟用，您必須按一下**停用**，然後按一下**啟用**hello 使用者名稱和密碼，您可以變更之前...</span><span class="sxs-lookup"><span data-stu-id="f2bd9-271">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change hello username and password..</span></span>
5. <span data-ttu-id="f2bd9-272">變更 hello**叢集登入名稱**及/或 hello**叢集登入密碼**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-272">Change hello **Cluster Login Name** and/or hello **Cluster Login Password**, and then click **Save**.</span></span>

    ![HDInsight change cluster user username password http user](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a><span data-ttu-id="f2bd9-274">授與/撤銷存取權</span><span class="sxs-lookup"><span data-stu-id="f2bd9-274">Grant/revoke access</span></span>
<span data-ttu-id="f2bd9-275">HDInsight 叢集都有下列 （所有這些服務有 RESTful 端點） 的 HTTP web 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2bd9-275">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="f2bd9-276">ODBC</span><span class="sxs-lookup"><span data-stu-id="f2bd9-276">ODBC</span></span>
* <span data-ttu-id="f2bd9-277">JDBC</span><span class="sxs-lookup"><span data-stu-id="f2bd9-277">JDBC</span></span>
* <span data-ttu-id="f2bd9-278">Ambari</span><span class="sxs-lookup"><span data-stu-id="f2bd9-278">Ambari</span></span>
* <span data-ttu-id="f2bd9-279">Oozie</span><span class="sxs-lookup"><span data-stu-id="f2bd9-279">Oozie</span></span>
* <span data-ttu-id="f2bd9-280">Templeton</span><span class="sxs-lookup"><span data-stu-id="f2bd9-280">Templeton</span></span>

<span data-ttu-id="f2bd9-281">預設會授與這些服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-281">By default, these services are granted for access.</span></span> <span data-ttu-id="f2bd9-282">您可以撤銷/授與 hello 存取從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-282">You can revoke/grant hello access from hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f2bd9-283">授與/撤銷 hello 存取權，您將會重設 hello 叢集使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-283">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="f2bd9-284">**toogrant/revoke HTTP web 服務存取**</span><span class="sxs-lookup"><span data-stu-id="f2bd9-284">**toogrant/revoke HTTP web services access**</span></span>

1. <span data-ttu-id="f2bd9-285">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-285">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f2bd9-286">按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-286">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="f2bd9-287">按一下**設定**從 hello 最上層功能表，然後再按一下**叢集登入**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-287">Click **Settings** from hello top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="f2bd9-288">如果**叢集登入**已啟用，您必須按一下**停用**，然後按一下**啟用**hello 使用者名稱和密碼，您可以變更之前...</span><span class="sxs-lookup"><span data-stu-id="f2bd9-288">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change hello username and password..</span></span>
5. <span data-ttu-id="f2bd9-289">如**叢集登入使用者名稱**和**叢集登入密碼**，hello 叢集分別輸入 hello 新的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-289">For **Cluster Login Username** and **Cluster Login Password**, enter hello new user name and password (respectively) for hello cluster.</span></span>
6. <span data-ttu-id="f2bd9-290">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-290">Click **SAVE**.</span></span>

    ![HDInsight grand remove http web service access](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="f2bd9-292">找不到 hello 預設儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f2bd9-292">Find hello default storage account</span></span>
<span data-ttu-id="f2bd9-293">每個 HDInsight 叢集都有預設的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-293">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="f2bd9-294">叢集會顯示在 hello 預設儲存體帳戶，而且其索引鍵**設定**/**屬性**/**Azure 儲存體金鑰**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-294">hello default storage account and its keys for a cluster appears under **Settings**/**Properties**/**Azure Storage Keys**.</span></span> <span data-ttu-id="f2bd9-295">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-295">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-hello-resource-group"></a><span data-ttu-id="f2bd9-296">找不到 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="f2bd9-296">Find hello resource group</span></span>
<span data-ttu-id="f2bd9-297">在 hello Azure Resource Manager 模式中，每個 HDInsight 叢集建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-297">In hello Azure Resource Manager mode, each HDInsight cluster is created with an Azure resource group.</span></span> <span data-ttu-id="f2bd9-298">叢集所屬 tooappears 中的 hello Azure 資源群組：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-298">hello Azure resource group that a cluster belongs tooappears in:</span></span>

* <span data-ttu-id="f2bd9-299">hello 叢集清單有**資源群組**資料行。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-299">hello cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="f2bd9-300">叢集 [基本資料]  磚。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-300">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="f2bd9-301">請參閱 [列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-301">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="open-hdinsight-query-console"></a><span data-ttu-id="f2bd9-302">開啟 HDInsight 查詢主控台</span><span class="sxs-lookup"><span data-stu-id="f2bd9-302">Open HDInsight Query console</span></span>
<span data-ttu-id="f2bd9-303">hello HDInsight 查詢主控台包含下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2bd9-303">hello HDInsight Query console includes hello following features:</span></span>

* <span data-ttu-id="f2bd9-304">**Hive 編輯器**：用於提交 Hive 工作的 GUI Web 介面。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-304">**Hive Editor**: A GUI web interface for submitting Hive jobs.</span></span>  <span data-ttu-id="f2bd9-305">請參閱[執行 Hive 查詢使用 hello 查詢主控台](hdinsight-hadoop-use-hive-query-console.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-305">See [Run Hive queries using hello Query Console](hdinsight-hadoop-use-hive-query-console.md).</span></span>

    ![HDInsight portal hive editor](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* <span data-ttu-id="f2bd9-307">**工作歷程記錄**：監視 Hadoop 工作。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-307">**Job history**: Monitor Hadoop jobs.</span></span>  

    ![HDInsight portal job history](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    <span data-ttu-id="f2bd9-309">按一下**查詢名稱**tooshow hello 詳細資料，包括工作屬性**工作查詢**，和 * * 作業輸出。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-309">Click **Query Name** tooshow hello details including Job properties, **Job Query**, and **Job Output.</span></span> <span data-ttu-id="f2bd9-310">您也可以下載 hello 查詢與 hello 輸出 tooyour 工作站。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-310">You can also download both hello query and hello output tooyour workstation.</span></span>
* <span data-ttu-id="f2bd9-311">**檔案瀏覽器**： 瀏覽 hello 預設儲存體帳戶和 hello 連結儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-311">**File Browser**: Browse hello default storage account and hello linked storage accounts.</span></span>

    ![HDInsight portal file browser browse](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    <span data-ttu-id="f2bd9-313">在 hello 螢幕擷取畫面，hello  **<Account>** 類型表示 hello 項目是 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-313">On hello screenshot, hello **<Account>** type indicates hello item is an Azure storage account.</span></span>  <span data-ttu-id="f2bd9-314">按一下 hello 帳戶名稱 toobrowse hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-314">Click hello account name toobrowse hello files.</span></span>
* <span data-ttu-id="f2bd9-315">**Hadoop UI**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-315">**Hadoop UI**.</span></span>

    ![HDInsight portal Hadoop UI](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    <span data-ttu-id="f2bd9-317">從「Hadoop UI」，您可以瀏覽檔案，並檢查記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-317">From **Hadoop UI*, you can browse files, and check logs.</span></span>
* <span data-ttu-id="f2bd9-318">**Yarn UI**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-318">**Yarn UI**.</span></span>

    ![HDInsight portal YARN UI](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a><span data-ttu-id="f2bd9-320">執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="f2bd9-320">Run Hive queries</span></span>
<span data-ttu-id="f2bd9-321">tooran Hive 工作從 hello 入口網站中，按一下**登錄區編輯器**主控台 hello HDInsight 查詢中。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-321">tooran Hive jobs from hello Portal, click **Hive Editor** in hello HDInsight Query console.</span></span> <span data-ttu-id="f2bd9-322">請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-322">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="f2bd9-323">監視工作</span><span class="sxs-lookup"><span data-stu-id="f2bd9-323">Monitor jobs</span></span>
<span data-ttu-id="f2bd9-324">toomonitor 工作，從 hello 入口網站中，按一下**作業歷程記錄**主控台 hello HDInsight 查詢中。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-324">toomonitor jobs from hello Portal, click **Job History** in hello HDInsight Query console.</span></span> <span data-ttu-id="f2bd9-325">請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-325">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="browse-files"></a><span data-ttu-id="f2bd9-326">瀏覽檔案</span><span class="sxs-lookup"><span data-stu-id="f2bd9-326">Browse files</span></span>
<span data-ttu-id="f2bd9-327">toobrowse 檔案儲存在 hello 預設儲存體帳戶及 hello 連結儲存體帳戶，請按一下**檔案瀏覽器**主控台 hello HDInsight 查詢中。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-327">toobrowse files stored in hello default storage account and hello linked storage accounts, click **File Browser** in hello HDInsight Query console.</span></span> <span data-ttu-id="f2bd9-328">請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-328">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

<span data-ttu-id="f2bd9-329">您也可以使用 hello**瀏覽檔案系統中 hello**公用程式的 hello **Hadoop UI** hello HDInsight 主控台中。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-329">You can also use hello **Browse hello file system** utility from hello **Hadoop UI** in hello HDInsight console.</span></span>  <span data-ttu-id="f2bd9-330">請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-330">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="f2bd9-331">監視叢集使用量</span><span class="sxs-lookup"><span data-stu-id="f2bd9-331">Monitor cluster usage</span></span>
<span data-ttu-id="f2bd9-332">hello**使用量**hello HDInsight 叢集刀鋒視窗的區段會顯示 hello 核心可用 tooyour HDInsight，搭配使用的訂用帳戶數目，以及 hello toothis 叢集以及其同時配置的核心數目的相關資訊配置給 hello 此叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-332">hello **Usage** section of hello HDInsight cluster blade displays information about hello number of cores available tooyour subscription for use with HDInsight, as well as hello number of cores allocated toothis cluster and how they are allocated for hello nodes within this cluster.</span></span> <span data-ttu-id="f2bd9-333">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-333">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2bd9-334">toomonitor hello 服務提供 hello HDInsight 叢集，您必須使用 Ambari Web 或 hello Ambari REST API。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-334">toomonitor hello services provided by hello HDInsight cluster, you must use Ambari Web or hello Ambari REST API.</span></span> <span data-ttu-id="f2bd9-335">如需使用 Ambari 的詳細資訊，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="f2bd9-335">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="open-hadoop-ui"></a><span data-ttu-id="f2bd9-336">開啟 Hadoop UI</span><span class="sxs-lookup"><span data-stu-id="f2bd9-336">Open Hadoop UI</span></span>
<span data-ttu-id="f2bd9-337">toomonitor hello 叢集、 瀏覽 hello 檔案系統，並檢查記錄檔中，按一下**Hadoop UI**主控台 hello HDInsight 查詢中。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-337">toomonitor hello cluster, browse hello file system, and check logs, click **Hadoop UI** in hello HDInsight Query console.</span></span> <span data-ttu-id="f2bd9-338">請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-338">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="open-yarn-ui"></a><span data-ttu-id="f2bd9-339">開啟 Yarn UI</span><span class="sxs-lookup"><span data-stu-id="f2bd9-339">Open Yarn UI</span></span>
<span data-ttu-id="f2bd9-340">toouse Yarn 使用者介面中，按一下**Yarn UI**主控台 hello HDInsight 查詢中。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-340">toouse Yarn user interface, click **Yarn UI** in hello HDInsight Query console.</span></span> <span data-ttu-id="f2bd9-341">請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-341">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="connect-tooclusters-using-rdp"></a><span data-ttu-id="f2bd9-342">Tooclusters 使用 RDP 的連接</span><span class="sxs-lookup"><span data-stu-id="f2bd9-342">Connect tooclusters using RDP</span></span>
<span data-ttu-id="f2bd9-343">為您提供在其建立 hello 叢集 hello 認證提供 toohello hello 叢集中，但不是 toohello 叢集本身透過遠端桌面服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-343">hello credentials for hello cluster that you provided at its creation give access toohello services on hello cluster, but not toohello cluster itself through Remote Desktop.</span></span> <span data-ttu-id="f2bd9-344">當您佈建叢集時或叢集佈建完成後，可以開啟遠端桌面存取。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-344">You can turn on Remote Desktop access when you provision a cluster or after a cluster is provisioned.</span></span> <span data-ttu-id="f2bd9-345">有關建立時啟用遠端桌面的 hello 指示，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-345">For hello instructions about enabling Remote Desktop at creation, see [Create HDInsight cluster](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="f2bd9-346">**tooenable 遠端桌面**</span><span class="sxs-lookup"><span data-stu-id="f2bd9-346">**tooenable Remote Desktop**</span></span>

1. <span data-ttu-id="f2bd9-347">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-347">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f2bd9-348">按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-348">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="f2bd9-349">按一下**設定**從 hello 最上層功能表，然後再按一下**遠端桌面**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-349">Click **Settings** from hello top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="f2bd9-350">輸入 到期日、遠端桌面使用者名稱 和 遠端桌面密碼，然後按一下啟用。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-350">Enter **Expires On**, **Remote Desktop Username** and **Remote Desktop Password**, and then click **Enable**.</span></span>

    ![HDInsight 啟用停用設定遠端桌面](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    <span data-ttu-id="f2bd9-352">hello 的到期日的預設值是一週。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-352">hello default values for Expires On is a week.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f2bd9-353">您也可以在叢集上使用 hello HDInsight.NET SDK tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-353">You can also use hello HDInsight .NET SDK tooenable Remote Desktop on a cluster.</span></span> <span data-ttu-id="f2bd9-354">使用 hello **EnableRdp** hello 下列方式中的 hello HDInsight 用戶端物件上的方法：**用戶端。EnableRdp (clustername、 位置、"rdpuser"、"rdppassword"，DateTime.Now.AddDays(6))**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-354">Use hello **EnableRdp** method on hello HDInsight client object in hello following manner: **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span></span> <span data-ttu-id="f2bd9-355">同樣地，toodisable 遠端桌面 hello 叢集上的，您可以使用**用戶端。DisableRdp （clustername、 位置）**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-355">Similarly, toodisable Remote Desktop on hello cluster, you can use **client.DisableRdp(clustername, location)**.</span></span> <span data-ttu-id="f2bd9-356">如需這些方法的詳細資訊，請參閱 [HDInsight .NET SDK 參考](http://go.microsoft.com/fwlink/?LinkId=529017)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-356">For more information on these methods, see [HDInsight .NET SDK Reference](http://go.microsoft.com/fwlink/?LinkId=529017).</span></span> <span data-ttu-id="f2bd9-357">這僅適用於在 Windows 上執行的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-357">This is applicable only for HDInsight clusters running on Windows.</span></span>
   >
   >

<span data-ttu-id="f2bd9-358">**使用 RDP tooconnect tooa 叢集**</span><span class="sxs-lookup"><span data-stu-id="f2bd9-358">**tooconnect tooa cluster by using RDP**</span></span>

1. <span data-ttu-id="f2bd9-359">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-359">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f2bd9-360">按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-360">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="f2bd9-361">按一下**設定**從 hello 最上層功能表，然後再按一下**遠端桌面**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-361">Click **Settings** from hello top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="f2bd9-362">按一下**連接**並遵循 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-362">Click **Connect** and follow hello instructions.</span></span> <span data-ttu-id="f2bd9-363">如果 [連接] 已停用，您必須先加以啟用。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-363">If Connect is disable, you must enable it first.</span></span> <span data-ttu-id="f2bd9-364">請確定使用 hello 遠端桌面使用者使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-364">Make sure using hello Remote Desktop user username and password.</span></span>  <span data-ttu-id="f2bd9-365">您無法使用 hello 叢集使用者認證。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-365">You can't use hello Cluster user credentials.</span></span>

## <a name="open-hadoop-command-line"></a><span data-ttu-id="f2bd9-366">開啟 Hadoop 命令列</span><span class="sxs-lookup"><span data-stu-id="f2bd9-366">Open Hadoop command line</span></span>
<span data-ttu-id="f2bd9-367">tooconnect toohello 叢集中，使用遠端桌面和使用 hello Hadoop 命令列，您必須先啟用遠端桌面存取 toohello 叢集 hello 上一節中所述。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-367">tooconnect toohello cluster by using Remote Desktop and use hello Hadoop command line, you must first have enabled Remote Desktop access toohello cluster as described in hello previous section.</span></span>

<span data-ttu-id="f2bd9-368">**tooopen Hadoop 命令列**</span><span class="sxs-lookup"><span data-stu-id="f2bd9-368">**tooopen a Hadoop command line**</span></span>

1. <span data-ttu-id="f2bd9-369">Toohello 叢集使用遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-369">Connect toohello cluster using Remote Desktop.</span></span>
2. <span data-ttu-id="f2bd9-370">從 hello 桌面按兩下**Hadoop 命令列**。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-370">From hello desktop, double-click **Hadoop Command Line**.</span></span>

    <span data-ttu-id="f2bd9-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span><span class="sxs-lookup"><span data-stu-id="f2bd9-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span></span>

    <span data-ttu-id="f2bd9-372">如需 Hadoop 命令的詳細資訊，請參閱 [Hadoop 命令參考](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html)。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-372">For more information on Hadoop commands, see [Hadoop commands reference](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span></span>

<span data-ttu-id="f2bd9-373">在 hello 上一個螢幕擷取畫面，hello 資料夾名稱會有內嵌的 hello Hadoop 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-373">In hello previous screenshot, hello folder name has hello Hadoop version number embedded.</span></span> <span data-ttu-id="f2bd9-374">hello 版本號碼可以變更根據的 hello hello 叢集上安裝的 hello Hadoop 元件版本。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-374">hello version number can changed based on hello version of hello Hadoop components installed on hello cluster.</span></span> <span data-ttu-id="f2bd9-375">您可以使用 Hadoop 環境變數 toorefer toothose 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-375">You can use Hadoop environment variables toorefer toothose folders.</span></span> <span data-ttu-id="f2bd9-376">例如：</span><span class="sxs-lookup"><span data-stu-id="f2bd9-376">For example:</span></span>

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a><span data-ttu-id="f2bd9-377">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2bd9-377">Next steps</span></span>
<span data-ttu-id="f2bd9-378">在本文中，您已經學會如何使用的 HDInsight 叢集 toocreate hello 入口網站，和如何 tooopen hello Hadoop 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="f2bd9-378">In this article, you have learned how toocreate an HDInsight cluster by using hello Portal, and how tooopen hello Hadoop command-line tool.</span></span> <span data-ttu-id="f2bd9-379">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="f2bd9-379">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="f2bd9-380">使用 Azure PowerShell 管理 HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2bd9-380">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="f2bd9-381">使用 Azure CLI 管理 HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2bd9-381">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="f2bd9-382">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f2bd9-382">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="f2bd9-383">以程式設計方式提交 Hadoop 工作</span><span class="sxs-lookup"><span data-stu-id="f2bd9-383">Submit Hadoop jobs programmatically</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* [<span data-ttu-id="f2bd9-384">開始使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2bd9-384">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="f2bd9-385">Azure HDInsight 提供 Hadoop 的什麼版本？</span><span class="sxs-lookup"><span data-stu-id="f2bd9-385">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop 命令列"
