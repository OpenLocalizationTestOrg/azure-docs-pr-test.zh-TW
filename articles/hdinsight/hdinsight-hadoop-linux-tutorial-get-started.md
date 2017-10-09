---
title: "aaaGet 入門 Hadoop 和 Azure HDInsight 中的登錄區 |Microsoft 文件"
description: "了解如何 toocreate HDInsight 叢集，以及使用 Hive 查詢資料。"
keywords: "開始使用,hadoop linux,hadoop 快速入門,開始使用 hive,hive 快速入門"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a><span data-ttu-id="9324d-104">Hadoop 教學課程：開始在 HDInsight 中使用 Hadoop</span><span class="sxs-lookup"><span data-stu-id="9324d-104">Hadoop tutorial: Get started using Hadoop in HDInsight</span></span>

<span data-ttu-id="9324d-105">深入了解如何 toocreate [Hadoop](http://hadoop.apache.org/) HDInsight 及 toorun Hive HDInsight 中的工作中的叢集。</span><span class="sxs-lookup"><span data-stu-id="9324d-105">Learn how toocreate [Hadoop](http://hadoop.apache.org/) clusters in HDInsight, and how toorun Hive jobs in HDInsight.</span></span> <span data-ttu-id="9324d-106">[Apache Hive](https://hive.apache.org/)是 hello hello Hadoop 生態系統中最受歡迎的元件。</span><span class="sxs-lookup"><span data-stu-id="9324d-106">[Apache Hive](https://hive.apache.org/) is hello most popular component in hello Hadoop ecosystem.</span></span> <span data-ttu-id="9324d-107">HDInsight 目前隨附 [7 個不同的叢集類型](hdinsight-hadoop-introduction.md#overview)。</span><span class="sxs-lookup"><span data-stu-id="9324d-107">Currently HDInsight comes with [seven different cluster types](hdinsight-hadoop-introduction.md#overview).</span></span> <span data-ttu-id="9324d-108">每種叢集類型都支援一組不同的元件。</span><span class="sxs-lookup"><span data-stu-id="9324d-108">Each cluster type supports a different set of components.</span></span> <span data-ttu-id="9324d-109">所有叢集類型都支援 Hive。</span><span class="sxs-lookup"><span data-stu-id="9324d-109">All cluster types support Hive.</span></span> <span data-ttu-id="9324d-110">如需支援的元件，在 HDInsight 中的清單，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="9324d-110">For a list of supported components in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</span></span>  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="9324d-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="9324d-111">Prerequisites</span></span>
<span data-ttu-id="9324d-112">開始進行本教學課程之前，您必須具備：</span><span class="sxs-lookup"><span data-stu-id="9324d-112">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="9324d-113">**Azure 訂用帳戶**: toocreate 免費的一個月試用版帳戶，瀏覽過[azure.microsoft.com/free](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="9324d-113">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>

## <a name="create-cluster"></a><span data-ttu-id="9324d-114">建立叢集</span><span class="sxs-lookup"><span data-stu-id="9324d-114">Create cluster</span></span>

<span data-ttu-id="9324d-115">大部分 Hadoop 作業都是批次作業。</span><span class="sxs-lookup"><span data-stu-id="9324d-115">Most of Hadoop jobs are batch jobs.</span></span> <span data-ttu-id="9324d-116">您會建立叢集，執行某些作業，然後再刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="9324d-116">You create a cluster, run some jobs, and then delete hello cluster.</span></span> <span data-ttu-id="9324d-117">在本節中，您會在 HDInsight 中使用 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)建立 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="9324d-117">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="9324d-118">進行本教學課程並不需要具備 Resource Manager 範本經驗。</span><span class="sxs-lookup"><span data-stu-id="9324d-118">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="9324d-119">適用於其他叢集建立方法，並了解本教學課程中使用的 hello 內容，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-119">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="9324d-120">使用 hello 選取器 hello hello 頁面 toochoose 頂端上您的叢集建立選項。</span><span class="sxs-lookup"><span data-stu-id="9324d-120">Use hello selector on hello top of hello page toochoose your cluster creation options.</span></span>

<span data-ttu-id="9324d-121">在本教學課程中使用的 hello Resource Manager 範本位於[GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)。</span><span class="sxs-lookup"><span data-stu-id="9324d-121">hello Resource Manager template used in this tutorial is located in [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> 

1. <span data-ttu-id="9324d-122">按一下下列 tooAzure 中的映像 toosign 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="9324d-122">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="9324d-123">輸入或選取下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="9324d-123">Enter or select hello following values:</span></span>
   
    <span data-ttu-id="9324d-124">![HDInsight Linux get 入口網站上啟動資源管理員範本](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "部署 Hadoop 叢集中使用 HDInsigut hello Azure 入口網站和資源群組管理員範本")。</span><span class="sxs-lookup"><span data-stu-id="9324d-124">![HDInsight Linux get started Resource Manager template on portal](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "Deploy Hadoop cluster in HDInsigut using hello Azure portal and a resource group manager template").</span></span>
   
    * <span data-ttu-id="9324d-125">**訂用帳戶**：選取您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9324d-125">**Subscription**: Select your Azure subscription.</span></span>
    * <span data-ttu-id="9324d-126">**資源群組**：建立資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9324d-126">**Resource group**: Create a resource group or select an existing resource group.</span></span>  <span data-ttu-id="9324d-127">資源群組是 Azure 元件的容器。</span><span class="sxs-lookup"><span data-stu-id="9324d-127">A resource group is a container of Azure components.</span></span>  <span data-ttu-id="9324d-128">在此情況下，hello 資源群組包含 hello HDInsight 叢集和 hello 相依的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9324d-128">In this case, hello resource group contains hello HDInsight cluster and hello dependent Azure Storage account.</span></span> 
    * <span data-ttu-id="9324d-129">**位置**： 選取您想 toocreate 您叢集的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="9324d-129">**Location**: Select an Azure location where you want toocreate your cluster.</span></span>  <span data-ttu-id="9324d-130">選擇位置較接近 tooyou 以提升效能。</span><span class="sxs-lookup"><span data-stu-id="9324d-130">Choose a location closer tooyou for better performance.</span></span> 
    * <span data-ttu-id="9324d-131">**叢集類型**：請為本教學課程選取 [hadoop]。</span><span class="sxs-lookup"><span data-stu-id="9324d-131">**Cluster Type**: Select **hadoop** for this tutorial.</span></span>
    * <span data-ttu-id="9324d-132">**叢集名稱**： 輸入 hello Hadoop 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="9324d-132">**Cluster Name**: Enter a name for hello Hadoop cluster.</span></span>
    * <span data-ttu-id="9324d-133">**叢集登入名稱和密碼**: hello 預設登入名稱是**admin**。</span><span class="sxs-lookup"><span data-stu-id="9324d-133">**Cluster login name and password**: hello default login name is **admin**.</span></span>
    * <span data-ttu-id="9324d-134">**SSH 使用者名稱和密碼**: hello 預設使用者名稱是**sshuser**。</span><span class="sxs-lookup"><span data-stu-id="9324d-134">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="9324d-135">您可以將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="9324d-135">You can rename it.</span></span> 
     
    <span data-ttu-id="9324d-136">某些屬性已被硬式編碼 hello 範本中。</span><span class="sxs-lookup"><span data-stu-id="9324d-136">Some properties have been hardcoded in hello template.</span></span>  <span data-ttu-id="9324d-137">您可以設定這些值從 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="9324d-137">You can configure these values from hello template.</span></span>

    * <span data-ttu-id="9324d-138">**位置**: hello hello 叢集的位置和 hello 相依的儲存體帳戶共用 hello 與 hello 資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="9324d-138">**Location**: hello location of hello cluster and hello dependent storage account share hello same location as hello resource group.</span></span>
    * <span data-ttu-id="9324d-139">**叢集版本**：3.5</span><span class="sxs-lookup"><span data-stu-id="9324d-139">**Cluster version**: 3.5</span></span>
    * <span data-ttu-id="9324d-140">**OS 類型**：Linux</span><span class="sxs-lookup"><span data-stu-id="9324d-140">**OS Type**: Linux</span></span>
    * <span data-ttu-id="9324d-141">**背景工作節點數目**：2</span><span class="sxs-lookup"><span data-stu-id="9324d-141">**Number of worker nodes**: 2</span></span>

     <span data-ttu-id="9324d-142">每個叢集都具備 [Azure 儲存體帳戶](hdinsight-hadoop-use-blob-storage.md)或 [Azure Data Lake 帳戶](hdinsight-hadoop-use-data-lake-store.md)相依性。</span><span class="sxs-lookup"><span data-stu-id="9324d-142">Each cluster has an [Azure Storage account](hdinsight-hadoop-use-blob-storage.md) or an [Azure Data Lake account](hdinsight-hadoop-use-data-lake-store.md) dependency.</span></span> <span data-ttu-id="9324d-143">它會稱為 hello 預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9324d-143">It is referred as hello default storage account.</span></span> <span data-ttu-id="9324d-144">HDInsight 叢集和其預設儲存體帳戶必須共置於 hello 中相同的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="9324d-144">HDInsight cluster and its default storage account must be co-located in hello same Azure region.</span></span> <span data-ttu-id="9324d-145">刪除叢集不會刪除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9324d-145">Deleting clusters does not delete hello storage account.</span></span> 
     
     <span data-ttu-id="9324d-146">如需這些屬性的詳細說明，請參閱[在 HDInsight 中建立Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-146">For more explanation of these properties, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

3. <span data-ttu-id="9324d-147">選取**toohello 條款和條件前面所述，即表示我同意**和**Pin toodashboard**，然後按一下**購買**。</span><span class="sxs-lookup"><span data-stu-id="9324d-147">Select **I agree toohello terms and conditions stated above** and **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="9324d-148">您應該會看到標題為新的圖格**部署範本部署**hello 入口網站儀表板上。</span><span class="sxs-lookup"><span data-stu-id="9324d-148">You shall see a new tile titled **Deploying Template deployment** on hello portal dashboard.</span></span> <span data-ttu-id="9324d-149">大約需要約 20 分鐘 toocreate 叢集。</span><span class="sxs-lookup"><span data-stu-id="9324d-149">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="9324d-150">一旦建立 hello 叢集後，hello 磚的 hello 標題是變更的 toohello 您指定的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="9324d-150">Once hello cluster is created, hello caption of hello tile is changed toohello resource group name you specified.</span></span> <span data-ttu-id="9324d-151">和 hello 入口網站會自動開啟 hello 資源群組中的新刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9324d-151">And hello portal automatically opens hello resource group in a new blade.</span></span> <span data-ttu-id="9324d-152">您可以看到 hello 叢集和 hello 所列的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="9324d-152">You can see both hello cluster and hello default storage listed.</span></span>
   
    <span data-ttu-id="9324d-153">![HDInsight Linux 開始使用的資源群組](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight 叢集資源群組")。</span><span class="sxs-lookup"><span data-stu-id="9324d-153">![HDInsight Linux get started resource group](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight cluster resource group").</span></span>

4. <span data-ttu-id="9324d-154">按一下 hello 叢集名稱 tooopen hello 叢集的新刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="9324d-154">Click hello cluster name tooopen hello cluster in a new blade.</span></span>

   <span data-ttu-id="9324d-155">![HDInsight Linux 開始使用的叢集設定](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "Azure HDInsight 屬性")</span><span class="sxs-lookup"><span data-stu-id="9324d-155">![HDInsight Linux get started cluster settings](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "HDInsight cluster properties")</span></span>


## <a name="run-hive-queries"></a><span data-ttu-id="9324d-156">執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="9324d-156">Run Hive queries</span></span>
<span data-ttu-id="9324d-157">[Apache Hive](hdinsight-use-hive.md)是 hello 最受歡迎使用 HDInsight 中的元件。</span><span class="sxs-lookup"><span data-stu-id="9324d-157">[Apache Hive](hdinsight-use-hive.md) is hello most popular component used in HDInsight.</span></span> <span data-ttu-id="9324d-158">有很多種 toorun Hive 工作在 HDInsight 中。</span><span class="sxs-lookup"><span data-stu-id="9324d-158">There are many ways toorun Hive jobs in HDInsight.</span></span> <span data-ttu-id="9324d-159">在本教學課程中，您可以使用 hello Ambari Hive 檢視從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9324d-159">In this tutorial, you use hello Ambari Hive view from hello portal.</span></span> <span data-ttu-id="9324d-160">如需提交 Hive 工作的其他方法，請參閱 [在 HDInsight 中使用 Hive](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-160">For other methods for submitting Hive jobs, see [Use Hive in HDInsight](hdinsight-use-hive.md).</span></span>

1. <span data-ttu-id="9324d-161">從 hello 上一個螢幕擷取畫面，按一下 **叢集儀表板**，然後按一下 **HDInsight 叢集儀表板**。</span><span class="sxs-lookup"><span data-stu-id="9324d-161">From hello previous screenshot, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span>  <span data-ttu-id="9324d-162">您也可以瀏覽過**https://&lt;ClusterName >。.azurehdinsight.net**，其中&lt;ClusterName > 是您在前一個區段 tooopen hello Ambari 建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="9324d-162">You can also browse too **https://&lt;ClusterName>.azurehdinsight.net**, where &lt;ClusterName> is hello cluster you created in hello previous section tooopen Ambari.</span></span>
2. <span data-ttu-id="9324d-163">輸入 hello Hadoop 使用者名稱和您在 hello 上一節中指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="9324d-163">Enter hello Hadoop username and password that you specified in hello previous section.</span></span> <span data-ttu-id="9324d-164">hello 預設使用者名稱是**admin**。</span><span class="sxs-lookup"><span data-stu-id="9324d-164">hello default username is **admin**.</span></span>
3. <span data-ttu-id="9324d-165">開啟**Hive 檢視**hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="9324d-165">Open **Hive View** as shown in hello following screenshot:</span></span>
   
    <span data-ttu-id="9324d-166">![選取 Ambari 檢視](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive 檢視器功能表")。</span><span class="sxs-lookup"><span data-stu-id="9324d-166">![Selecting Ambari views](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive Viwer menu").</span></span>
4. <span data-ttu-id="9324d-167">在 [hello**查詢編輯器**hello] 頁面上，貼上下列 HiveQL 陳述式 hello 工作表中的 hello 區段：</span><span class="sxs-lookup"><span data-stu-id="9324d-167">In hello **Query Editor** section of hello page, paste hello following HiveQL statements into hello worksheet:</span></span>
   
        SHOW TABLES;
   
   > [!NOTE]
   > <span data-ttu-id="9324d-168">Hive 需要分號。</span><span class="sxs-lookup"><span data-stu-id="9324d-168">Semi-colon is required by Hive.</span></span>       
   > 
   > 
5. <span data-ttu-id="9324d-169">按一下 [Execute (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="9324d-169">Click **Execute**.</span></span> <span data-ttu-id="9324d-170">A**查詢程序結果**區段應該會顯示在底下 hello 查詢編輯器，並顯示 hello 工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9324d-170">A **Query Process Results** section should appear beneath hello Query Editor and display information about hello job.</span></span> 
   
    <span data-ttu-id="9324d-171">Hello 查詢完成時，一旦 hello**查詢程序結果**區段會顯示 hello hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="9324d-171">Once hello query has finished, hello **Query Process Results** section displays hello results of hello operation.</span></span> <span data-ttu-id="9324d-172">您應該會看到一個名為 hivesampletable 的資料表。</span><span class="sxs-lookup"><span data-stu-id="9324d-172">You shall see one table called **hivesampletable**.</span></span> <span data-ttu-id="9324d-173">此範例的 Hive 資料表隨附於所有的 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9324d-173">This sample Hive table comes with all hello HDInsight clusters.</span></span>
   
    <span data-ttu-id="9324d-174">![HDInsight Hive 檢視](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive 檢視查詢編輯器")。</span><span class="sxs-lookup"><span data-stu-id="9324d-174">![HDInsight Hive views](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive View Query Editor").</span></span>
6. <span data-ttu-id="9324d-175">重複步驟 4 和 5 步驟 toorun hello 下列查詢：</span><span class="sxs-lookup"><span data-stu-id="9324d-175">Repeat step 4 and step 5 toorun hello following query:</span></span>
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > <span data-ttu-id="9324d-176">請注意 hello**將結果儲存**下拉式清單中 hello 右上方 hello**查詢程序結果**區段; 您可以使用這個 tooeither 下載 hello 的結果，或將它們儲存 tooHDInsight 儲存成 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="9324d-176">Note hello **Save results** dropdown in hello upper left of hello **Query Process Results** section; you can use this tooeither download hello results, or save them tooHDInsight storage as a CSV file.</span></span>
   > 
   > 
7. <span data-ttu-id="9324d-177">按一下**記錄**tooget hello 工作清單。</span><span class="sxs-lookup"><span data-stu-id="9324d-177">Click **History** tooget a list of hello jobs.</span></span>

<span data-ttu-id="9324d-178">您已完成的 Hive 工作之後，您可以[hello 結果 tooAzure SQL 資料庫或 SQL Server 資料庫匯出](hdinsight-use-sqoop-mac-linux.md)，您也可以[將使用 Excel 的 hello 結果視覺化](hdinsight-connect-excel-power-query.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-178">After you have completed a Hive job, you can [export hello results tooAzure SQL database or SQL Server database](hdinsight-use-sqoop-mac-linux.md), you can also [visualize hello results using Excel](hdinsight-connect-excel-power-query.md).</span></span> <span data-ttu-id="9324d-179">如需使用 HDInsight 中的登錄區的詳細資訊，請參閱[使用 Hive 和 HiveQL HDInsight tooanalyze 範例 Apache log4j 檔案中的 Hadoop](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-179">For more information about using Hive in HDInsight, see [Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file](hdinsight-use-hive.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="9324d-180">清除 hello 教學課程</span><span class="sxs-lookup"><span data-stu-id="9324d-180">Clean up hello tutorial</span></span>
<span data-ttu-id="9324d-181">完成 hello 教學課程之後，您可能想 toodelete hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="9324d-181">After you complete hello tutorial, you may want toodelete hello cluster.</span></span> <span data-ttu-id="9324d-182">利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。</span><span class="sxs-lookup"><span data-stu-id="9324d-182">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="9324d-183">您也需支付 HDInsight 叢集的費用 (即使未使用)。</span><span class="sxs-lookup"><span data-stu-id="9324d-183">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="9324d-184">由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。</span><span class="sxs-lookup"><span data-stu-id="9324d-184">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> 

> [!NOTE]
> <span data-ttu-id="9324d-185">使用[Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md)，您可以視情況下，需要建立 HDInsight 叢集並設定 TimeToLive 設定太 hello 叢集自動刪除。</span><span class="sxs-lookup"><span data-stu-id="9324d-185">Using [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md), you can create HDInsight clusters on demand, and configure a TimeToLive setting too delete hello clusters automatically.</span></span> 
> 
> 

<span data-ttu-id="9324d-186">**toodelete hello 叢集及/或 hello 預設儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="9324d-186">**toodelete hello cluster and/or hello default storage account**</span></span>

1. <span data-ttu-id="9324d-187">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9324d-187">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9324d-188">從 hello 入口網站儀表板，按一下 hello 磚 hello 建立 hello 叢集時，使用的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="9324d-188">From hello portal dashboard, click hello tile with hello resource group name you used when you created hello cluster.</span></span>
3. <span data-ttu-id="9324d-189">按一下**刪除**在 hello 資源刀鋒視窗 toodelete hello 資源群組，其中包含 hello 叢集和 hello 預設儲存體帳戶，或按一下 hello 叢集名稱上 hello**資源**磚，然後按一下**刪除**hello 叢集刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="9324d-189">Click **Delete** on hello resource blade toodelete hello resource group, which contains hello cluster and hello default storage account; or click hello cluster name on hello **Resources** tile and then click **Delete** on hello cluster blade.</span></span> <span data-ttu-id="9324d-190">請注意，刪除 hello 資源群組中刪除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9324d-190">Note deleting hello resource group deletes hello storage account.</span></span> <span data-ttu-id="9324d-191">如果您想 tookeep hello 儲存體帳戶，請選擇 toodelete hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="9324d-191">If you want tookeep hello storage account, choose toodelete hello cluster only.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="9324d-192">疑難排解</span><span class="sxs-lookup"><span data-stu-id="9324d-192">Troubleshoot</span></span>

<span data-ttu-id="9324d-193">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="9324d-193">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9324d-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9324d-194">Next steps</span></span>
<span data-ttu-id="9324d-195">在本教學課程中，您已經學會如何 toocreate 以 Linux 為基礎的 HDInsight 叢集使用資源管理員範本，以及如何 tooperform 基本 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="9324d-195">In this tutorial, you have learned how toocreate a Linux-based HDInsight cluster using a Resource Manager template, and how tooperform basic Hive queries.</span></span>

<span data-ttu-id="9324d-196">toolearn 有關使用 HDInsight，分析資料的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="9324d-196">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="9324d-197">toolearn 更多有關搭配使用 Hive 與 HDInsight，包括如何 tooperform Hive 查詢從 Visual Studio，請參閱[使用 Hive 與 HDInsight][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="9324d-197">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="9324d-198">關於 Pig toolearn，使用語言 tootransform 資料，請參閱[與 HDInsight 搭配使用 Pig][hdinsight-use-pig]。</span><span class="sxs-lookup"><span data-stu-id="9324d-198">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="9324d-199">toolearn 有關 MapReduce，方式 toowrite 程式的處理資料的 Hadoop，請參閱[與 HDInsight 的使用 MapReduce][hdinsight-use-mapreduce]。</span><span class="sxs-lookup"><span data-stu-id="9324d-199">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="9324d-200">請參閱有關使用 hello HDInsight Tools for Visual Studio tooanalyze 資料在 HDInsight 上 toolearn[開始使用 Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-200">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="9324d-201">如果您是使用您自己的資料準備 toostart，且需要深入了解 tooknow HDInsight 儲存資料的方式，或如何 tooget 資料 HDInsight，請參閱下列資訊 hello:</span><span class="sxs-lookup"><span data-stu-id="9324d-201">If you're ready toostart working with your own data and need tooknow more about how HDInsight stores data or how tooget data into HDInsight, see hello following:</span></span>

* <span data-ttu-id="9324d-202">如需有關 HDInsight 如何使用 Azure 儲存體的資訊，請參閱 [搭配 HDInsight 使用 Azure 儲存體](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-202">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="9324d-203">如需詳細資訊 tooupload 資料 tooHDInsight，請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="9324d-203">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="9324d-204">如果您想要 toolearn 深入了解建立或管理的 HDInsight 叢集，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="9324d-204">If you'd like toolearn more about creating or managing an HDInsight cluster, see hello following:</span></span>

* <span data-ttu-id="9324d-205">toolearn 關於管理您的 Linux 為基礎的 HDInsight 叢集，請參閱[使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-205">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="9324d-206">toolearn 進一步了解 hello 選項，您可以選取當建立 HDInsight 叢集，請參閱[建立使用自訂選項的 Linux 的 HDInsight](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-206">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="9324d-207">如果您熟悉 Linux 及 Hadoop，但是想 tooknow 特點 Hadoop hello HDInsight 上的時，請參閱[Linux 上使用 HDInsight](hdinsight-hadoop-linux-information.md)。</span><span class="sxs-lookup"><span data-stu-id="9324d-207">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="9324d-208">本文提供的資訊如下：</span><span class="sxs-lookup"><span data-stu-id="9324d-208">This article provides information such as:</span></span>
  
  * <span data-ttu-id="9324d-209">裝載在 hello 叢集上，例如 Ambari 和 WebHCat 服務的 Url</span><span class="sxs-lookup"><span data-stu-id="9324d-209">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="9324d-210">hello 位置的 Hadoop 檔案與 hello 本機檔案系統上的範例</span><span class="sxs-lookup"><span data-stu-id="9324d-210">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="9324d-211">hello 使用的 Azure 儲存體 (WASB) 而不是 HDFS 做 hello 預設資料存放區</span><span class="sxs-lookup"><span data-stu-id="9324d-211">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


