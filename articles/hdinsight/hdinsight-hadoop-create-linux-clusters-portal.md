---
title: "使用網頁瀏覽器-Azure HDInsight aaaCreate Hadoop 叢集 |Microsoft 文件"
description: "了解如何 toocreate Hadoop、 HBase、 風暴或 Spark 叢集在 Linux 上使用網頁瀏覽器的 hdinsight 和 hello Azure preview 入口網站。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a><span data-ttu-id="e892e-103">HDInsight 使用 hello Azure 入口網站中建立以 Linux 為基礎的叢集</span><span class="sxs-lookup"><span data-stu-id="e892e-103">Create Linux-based clusters in HDInsight using hello Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="e892e-104">hello Azure 入口網站是服務和資源 hello Microsoft Azure 雲端中裝載的網頁型管理工具。</span><span class="sxs-lookup"><span data-stu-id="e892e-104">hello Azure portal is a web-based management tool for services and resources hosted in hello Microsoft Azure cloud.</span></span> <span data-ttu-id="e892e-105">本文中，您將學習如何 toocreate 以 Linux 為基礎的 HDInsight 叢集使用 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e892e-105">In this article you will learn how toocreate Linux-based HDInsight clusters using hello portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e892e-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="e892e-106">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="e892e-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e892e-107">**An Azure subscription**.</span></span> <span data-ttu-id="e892e-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="e892e-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e892e-109">**現代 Web 瀏覽器**。</span><span class="sxs-lookup"><span data-stu-id="e892e-109">**A modern web browser**.</span></span> <span data-ttu-id="e892e-110">hello Azure 入口網站會使用 HTML5 和 Javascript，並可能無法正確執行較舊的網頁瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="e892e-110">hello Azure  portal uses HTML5 and Javascript, and may not function correctly in older web browsers.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="e892e-111">建立叢集</span><span class="sxs-lookup"><span data-stu-id="e892e-111">Create clusters</span></span>
<span data-ttu-id="e892e-112">hello Azure 入口網站會公開大部分的 hello 叢集內容。</span><span class="sxs-lookup"><span data-stu-id="e892e-112">hello Azure portal exposes most of hello cluster properties.</span></span> <span data-ttu-id="e892e-113">使用 Azure Resource Manager 範本，您可以隱藏許多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e892e-113">Using Azure Resource Manager template, you can hide a lot of details.</span></span> <span data-ttu-id="e892e-114">如需詳細資訊，請參閱 [使用 Azure Resource Manager 範本在 HDInsight 中建立 Linux 型的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-114">For more information, see [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. <span data-ttu-id="e892e-115">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e892e-115">Sign in toohello [Azure  portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e892e-116">依序按一下 [+]、[智慧 + 分析] 及 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="e892e-116">Click **+**, click **Intelligence + Analytics**, and then click **HDInsight**.</span></span>
   
    <span data-ttu-id="e892e-117">![在 hello Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "hello Azure 入口網站中建立新的叢集")</span><span class="sxs-lookup"><span data-stu-id="e892e-117">![Creating a new cluster in hello Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "Creating a new cluster in hello Azure portal")</span></span>

3. <span data-ttu-id="e892e-118">在 hello **HDInsight**刀鋒視窗中，按一下**（大小、 設定、 應用程式） 的自訂**，按一下**基本概念**，然後輸入下列資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="e892e-118">In hello **HDInsight** blade, click **Custom (size, settings, apps)**, click **Basics**, and then enter hello following information.</span></span>

    <span data-ttu-id="e892e-119">![在 hello Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "hello Azure 入口網站中建立新的叢集")</span><span class="sxs-lookup"><span data-stu-id="e892e-119">![Creating a new cluster in hello Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "Creating a new cluster in hello Azure portal")</span></span>

    * <span data-ttu-id="e892e-120">輸入 **叢集名稱**：此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="e892e-120">Enter **Cluster Name**: This name must be globally unique.</span></span>

    * <span data-ttu-id="e892e-121">從 hello**訂用帳戶**下拉式清單中，選取 hello hello 叢集將使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e892e-121">From hello **Subscription** drop-down, select hello Azure subscription that will be used for hello cluster.</span></span>

    * <span data-ttu-id="e892e-122">按一下 [叢集類型]，然後選取：</span><span class="sxs-lookup"><span data-stu-id="e892e-122">Click **Cluster type**, and then select:</span></span>
   
        * <span data-ttu-id="e892e-123">**叢集類型**： 如果您不知道哪些 toochoose，選取**Hadoop**。</span><span class="sxs-lookup"><span data-stu-id="e892e-123">**Cluster Type**: If you don't know what toochoose, select **Hadoop**.</span></span> <span data-ttu-id="e892e-124">它是 hello 最受歡迎的叢集類型。</span><span class="sxs-lookup"><span data-stu-id="e892e-124">It is hello most popular cluster type.</span></span>
     
            > [!IMPORTANT]
            > <span data-ttu-id="e892e-125">HDInsight 叢集有各種不同的類型，對應 toohello 工作負載或調整為 hello 叢集的技術。</span><span class="sxs-lookup"><span data-stu-id="e892e-125">HDInsight clusters come in a variety of types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="e892e-126">沒有任何支援的方法 toocreate 結合多個類型，例如 Storm 和上一個叢集的 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="e892e-126">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span> 
            > 
            > 
        
        * <span data-ttu-id="e892e-127">**作業系統**：選取 [Linux]。</span><span class="sxs-lookup"><span data-stu-id="e892e-127">**Operating System**: Select **Linux**.</span></span>
        
        * <span data-ttu-id="e892e-128">**版本**： 如果您不知道哪些 toochoose 使用 hello 預設版本。</span><span class="sxs-lookup"><span data-stu-id="e892e-128">**Version**: Use hello default version if you don't know what toochoose.</span></span> <span data-ttu-id="e892e-129">如需詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-129">For more information, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
        * <span data-ttu-id="e892e-130">**叢集層**: Azure HDInsight 提供 hello 巨量資料雲端供應項目兩種類型： 標準層和 Premium 層。</span><span class="sxs-lookup"><span data-stu-id="e892e-130">**Cluster Tier**: Azure HDInsight provides hello big data cloud offerings in two categories: Standard tier and Premium tier.</span></span> <span data-ttu-id="e892e-131">如需詳細資訊，請參閱 [叢集層](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers)。</span><span class="sxs-lookup"><span data-stu-id="e892e-131">For more information, see [Cluster tiers](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).</span></span>

    * <span data-ttu-id="e892e-132">如**叢集登入使用者名稱**和**叢集登入密碼**，提供 hello 使用者名稱和密碼 hello 系統管理使用者。</span><span class="sxs-lookup"><span data-stu-id="e892e-132">For **Cluster login username** and **Cluster login password**, provide hello username and password for hello admin user.</span></span>

    * <span data-ttu-id="e892e-133">輸入**SSH 使用者名稱**，如果您想 toohave hello SSH 密碼相同 hello 您稍早指定的系統管理員密碼，請選取 hello**使用與叢集登入相同的密碼**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e892e-133">Enter an **SSH Username** and if you want toohave hello SSH password same as hello admin password you specified earlier, select hello **Use same password as cluster login** check box.</span></span> <span data-ttu-id="e892e-134">如果沒有，請提供**密碼**或**公開金鑰**，這將會使用的 tooauthenticate hello SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="e892e-134">If not, provide either a **PASSWORD** or **PUBLIC KEY**, which will be used tooauthenticate hello SSH user.</span></span> <span data-ttu-id="e892e-135">使用公開金鑰為 hello 建議的方法。</span><span class="sxs-lookup"><span data-stu-id="e892e-135">Using a public key is hello recommended approach.</span></span> <span data-ttu-id="e892e-136">按一下**選取**在 hello 底部 toosave hello 認證組態。</span><span class="sxs-lookup"><span data-stu-id="e892e-136">Click **Select** at hello bottom toosave hello credentials configuration.</span></span>
   
        <span data-ttu-id="e892e-137">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-137">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    * <span data-ttu-id="e892e-138">如**資源群組**，指定是否要 toocreate 新的資源群組，或使用現有。</span><span class="sxs-lookup"><span data-stu-id="e892e-138">For **Resource group**, specify whether you want toocreate a new resource group or use an existing one.</span></span>

    * <span data-ttu-id="e892e-139">指定的資料中心**位置**hello 叢集將會建立。</span><span class="sxs-lookup"><span data-stu-id="e892e-139">Specify a data center **location** where hello cluster will be created.</span></span>

    * <span data-ttu-id="e892e-140">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="e892e-140">Click **Next**.</span></span>

4. <span data-ttu-id="e892e-141">在 hello**儲存體**刀鋒視窗中，指定您是要為您的預設儲存體 Azure 儲存體 (WASB) 還是資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="e892e-141">On hello **Storage** blade, specify whether you want Azure Storage (WASB) or Data Lake Store as your default storage.</span></span> <span data-ttu-id="e892e-142">查看 hello 下表中的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e892e-142">Look at hello table below for more information.</span></span>

    <span data-ttu-id="e892e-143">![在 hello Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "hello Azure 入口網站中建立新的叢集")</span><span class="sxs-lookup"><span data-stu-id="e892e-143">![Creating a new cluster in hello Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "Creating a new cluster in hello Azure portal")</span></span>

    | <span data-ttu-id="e892e-144">儲存體</span><span class="sxs-lookup"><span data-stu-id="e892e-144">Storage</span></span>                                      | <span data-ttu-id="e892e-145">說明</span><span class="sxs-lookup"><span data-stu-id="e892e-145">Description</span></span> |
    |----------------------------------------------|-------------|
    | <span data-ttu-id="e892e-146">**Azure 儲存體 Blob 做為預設儲存體**</span><span class="sxs-lookup"><span data-stu-id="e892e-146">**Azure Storage Blobs as default storage**</span></span>   | <ul><li><span data-ttu-id="e892e-147">對於 [主要儲存體類型]，請選取 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="e892e-147">For **Primary Storage type**, select **Azure Storage**.</span></span> <span data-ttu-id="e892e-148">在這之後，如**選取方法**，您可以選擇**我的訂閱**如果您想 toospecify 屬於您的 Azure 訂用帳戶的儲存體帳戶，然後選取 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e892e-148">After that, for **Selection method**, you can choose **My subscriptions** if you want toospecify a storage account that is part of your Azure subscription and then select hello storage account.</span></span> <span data-ttu-id="e892e-149">否則，請按一下**便捷鍵**，並提供 hello hello 的 toochoose 從您的 Azure 訂用帳戶以外的儲存體帳戶的資訊。</span><span class="sxs-lookup"><span data-stu-id="e892e-149">Otherwise, click **Access key** and provide hello information for hello storage account that you want toochoose from outside your Azure subscription.</span></span></li><li><span data-ttu-id="e892e-150">如**預設容器**，您可以選擇 toogo hello hello 入口網站所建議的預設容器名稱，或指定您自己。</span><span class="sxs-lookup"><span data-stu-id="e892e-150">For **Default container**, you can choose toogo with hello default container name suggested by hello portal or specify your own.</span></span></li><li><span data-ttu-id="e892e-151">如果您使用 WASB 作為預設儲存體，您可以 （選擇性） 按一下 **額外的儲存體帳戶**toospecify 額外的儲存體帳戶與 hello 叢集 tooassociate。</span><span class="sxs-lookup"><span data-stu-id="e892e-151">If you are using WASB as default storage, you can (optionally) click **Additional Storage Accounts** toospecify additional storage accounts tooassociate with hello cluster.</span></span> <span data-ttu-id="e892e-152">在 hello **Azure 儲存體金鑰**刀鋒視窗中，按一下 **新增儲存體金鑰**，然後您可以提供儲存體帳戶從您的 Azure 訂用帳戶或其他訂用帳戶 （藉由提供 hello 儲存體帳戶便捷鍵）。</span><span class="sxs-lookup"><span data-stu-id="e892e-152">In hello **Azure Storage Keys** blade, click **Add a storage key**, and then you can provide a storage account from your Azure subscriptions or from other subscriptions (by providing hello storage account access key).</span></span></li><li><span data-ttu-id="e892e-153">如果您使用 WASB 作為預設儲存體，您可以 （選擇性） 按一下 **資料湖存放區存取**toospecify 做為額外的儲存體的 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="e892e-153">If you are using WASB as default storage, you can (optionally) click **Data Lake Store access** toospecify Azure Data Lake Store as additional storage.</span></span> <span data-ttu-id="e892e-154">如需詳細資訊，請參閱[使用 Azure 入口網站建立具有 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-154">For more information, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span></li></ul> |
    | <span data-ttu-id="e892e-155">**Azure Data Lake Store 做為預設儲存體**</span><span class="sxs-lookup"><span data-stu-id="e892e-155">**Azure Data Lake Store as default storage**</span></span> | <span data-ttu-id="e892e-156">如**主要儲存體類型**，選取**Data Lake Store**然後再參閱 toohello 文章[建立與使用 Azure 入口網站的 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)的取得指示。</span><span class="sxs-lookup"><span data-stu-id="e892e-156">For **Primary storage type**, select **Data Lake Store** and then refer toohello article [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) for instructions.</span></span> |
    | <span data-ttu-id="e892e-157">**外部中繼存放區**</span><span class="sxs-lookup"><span data-stu-id="e892e-157">**External metastores**</span></span>                      | <span data-ttu-id="e892e-158">您可以選擇性地指定 SQL 資料庫 toosave Hive 和 Oozie 中繼資料與 hello 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="e892e-158">Optionally, you can specify a SQL database toosave Hive and Oozie metadata associated with hello cluster.</span></span> <span data-ttu-id="e892e-159">如**SQL database 選取的登錄區**選取 SQL 資料庫，然後再提供 hello 資料庫 hello 使用者名稱/密碼。</span><span class="sxs-lookup"><span data-stu-id="e892e-159">For **Select a SQL database for Hive** select a SQL database, and then provide hello username/password for hello database.</span></span> <span data-ttu-id="e892e-160">對 Oozie 中繼資料重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="e892e-160">Repeat these steps for Oozie metadata.</span></span><br><br><span data-ttu-id="e892e-161">針對中繼存放區使用 Azure SQL 資料庫時的一些考量。</span><span class="sxs-lookup"><span data-stu-id="e892e-161">Some considerations while using Azure SQL database for metastores.</span></span> <ul><li><span data-ttu-id="e892e-162">hello Azure SQL database 用於 hello 中繼存放區必須允許 Azure 服務，包括 Azure HDInsight 連線 tooother。</span><span class="sxs-lookup"><span data-stu-id="e892e-162">hello Azure SQL database used for hello metastore must allow connectivity tooother Azure services, including Azure HDInsight.</span></span> <span data-ttu-id="e892e-163">在 hello Azure SQL database 儀表板，在 hello 右邊，按一下 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="e892e-163">On hello Azure SQL database dashboard, on hello right side, click hello server name.</span></span> <span data-ttu-id="e892e-164">這是 hello 伺服器正在執行哪些 hello SQL 資料庫執行個體。</span><span class="sxs-lookup"><span data-stu-id="e892e-164">This is hello server on which hello SQL database instance is running.</span></span> <span data-ttu-id="e892e-165">當您在 hello 伺服器檢視，請按一下**設定**，然後**Azure 服務**，按一下**是**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="e892e-165">Once you are on hello server view, click **Configure**, and then for **Azure Services**, click **Yes**, and then click **Save**.</span></span></li><li><span data-ttu-id="e892e-166">在建立時的中繼存放區，請勿使用資料庫名稱包含破折號或連字號，這可能會導致 hello 叢集建立程序 toofail。</span><span class="sxs-lookup"><span data-stu-id="e892e-166">When creating a metastore, do not use a database name that contains dashes or hyphens, as this can cause hello cluster creation process toofail.</span></span></li></ul>                                                                                                                                                                       |

    <span data-ttu-id="e892e-167">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="e892e-167">Click **Next**.</span></span> 

    > [!WARNING]
    > <span data-ttu-id="e892e-168">不支援在 hello HDInsight 叢集以外的不同位置中使用額外的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e892e-168">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

5. <span data-ttu-id="e892e-169">（選擇性） 按一下**應用程式**tooinstall 應用程式使用的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e892e-169">Optionally, click **Applications** tooinstall applications that work with HDInsight clusters.</span></span> <span data-ttu-id="e892e-170">Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="e892e-170">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="e892e-171">如需詳細資訊，請參閱[安裝 HDInsight 應用程式](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation)。</span><span class="sxs-lookup"><span data-stu-id="e892e-171">For more information, see [Install HDInsight applications](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).</span></span>


6. <span data-ttu-id="e892e-172">按一下**叢集大小**toodisplay hello 節點將會建立此叢集的資訊。</span><span class="sxs-lookup"><span data-stu-id="e892e-172">Click **Cluster size** toodisplay information about hello nodes that will be created for this cluster.</span></span> <span data-ttu-id="e892e-173">設定 hello hello 叢集所需的背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="e892e-173">Set hello number of worker nodes that you need for hello cluster.</span></span> <span data-ttu-id="e892e-174">hello 估計成本的 hello 叢集將會顯示 hello 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="e892e-174">hello estimated cost of hello cluster will be shown within hello blade.</span></span>
   
    <span data-ttu-id="e892e-175">![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "指定叢集節點的數目")</span><span class="sxs-lookup"><span data-stu-id="e892e-175">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Specify number of cluster nodes")</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e892e-176">如果您計劃 32 個以上的背景工作節點，在叢集建立，或建立之後，調整 hello 叢集，則您必須選取前端節點大小至少為 8 個核心，14 GB ram。</span><span class="sxs-lookup"><span data-stu-id="e892e-176">If you plan on more than 32 worker nodes, either at cluster creation or by scaling hello cluster after creation, then you must select a head node size with at least 8 cores and 14GB ram.</span></span>
   > 
   > <span data-ttu-id="e892e-177">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="e892e-177">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   > 
   > 
   
   <span data-ttu-id="e892e-178">按一下**下一步**toosave hello 節點定價組態。</span><span class="sxs-lookup"><span data-stu-id="e892e-178">Click **Next** toosave hello node pricing configuration.</span></span>

7. <span data-ttu-id="e892e-179">按一下**進階設定**tooconfigure 其他選擇性設定，例如使用**指令碼動作**toocustomize 叢集 tooinstall 自訂元件，或加入**的虛擬網路**.</span><span class="sxs-lookup"><span data-stu-id="e892e-179">Click **Advanced settings** tooconfigure other optional settings such as using **Script Actions** toocustomize a cluster tooinstall custom components or joining a **Virtual Network**.</span></span> <span data-ttu-id="e892e-180">查看 hello 下表中的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e892e-180">Look at hello table below for more information.</span></span>

    <span data-ttu-id="e892e-181">![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "指定叢集節點的數目")</span><span class="sxs-lookup"><span data-stu-id="e892e-181">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Specify number of cluster nodes")</span></span>

    | <span data-ttu-id="e892e-182">選項</span><span class="sxs-lookup"><span data-stu-id="e892e-182">Option</span></span> | <span data-ttu-id="e892e-183">說明</span><span class="sxs-lookup"><span data-stu-id="e892e-183">Description</span></span> |
    |--------|-------------|
    | <span data-ttu-id="e892e-184">**指令碼動作**</span><span class="sxs-lookup"><span data-stu-id="e892e-184">**Script Actions**</span></span> | <span data-ttu-id="e892e-185">如果您想 toouse 自訂指令碼 toocustomize 叢集中，正在建立 hello 叢集時，使用此選項。</span><span class="sxs-lookup"><span data-stu-id="e892e-185">Use this option if you want toouse a custom script toocustomize a cluster, as hello cluster is being created.</span></span> <span data-ttu-id="e892e-186">如需指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-186">For more information about script actions, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span> |
    | <span data-ttu-id="e892e-187">**虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="e892e-187">**Virtual Network**</span></span> | <span data-ttu-id="e892e-188">如果您想要在虛擬網路的 tooplace hello 叢集，請選取 Azure 虛擬網路和 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="e892e-188">Select an Azure virtual network and hello subnet if you want tooplace hello cluster into a virtual network.</span></span> <span data-ttu-id="e892e-189">如需使用 HDInsight 與虛擬網路，包括特定組態需求的 hello 虛擬網路，請參閱[擴充 HDInsight 功能，方法是使用 Azure 虛擬網路](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-189">For information on using HDInsight with a Virtual Network, including specific configuration requirements for hello Virtual Network, see [Extend HDInsight capabilities by using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span> |

    <span data-ttu-id="e892e-190">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="e892e-190">Click **Next**.</span></span>

8. <span data-ttu-id="e892e-191">在 hello**摘要**刀鋒視窗中，確認您先前輸入的 hello 資訊，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="e892e-191">On hello **Summary** blade, verify hello information you entered earlier and then click **Create**.</span></span>

    <span data-ttu-id="e892e-192">![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "指定叢集節點的數目")</span><span class="sxs-lookup"><span data-stu-id="e892e-192">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Specify number of cluster nodes")</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e892e-193">它將需要一些時間 hello 叢集 toobe 建立，通常大約 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="e892e-193">It will take some time for hello cluster toobe created, usually around 15 minutes.</span></span> <span data-ttu-id="e892e-194">使用 hello 磚上 hello 開始面板，或 hello**通知**hello 上的項目上佈建程序的 hello 方 hello 頁面 toocheck。</span><span class="sxs-lookup"><span data-stu-id="e892e-194">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello provisioning process.</span></span>
    > 
    > 
12. <span data-ttu-id="e892e-195">Hello 建立程序完成之後，請按一下 hello 磚 hello 叢集 hello 開始面板 toolaunch hello 叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e892e-195">Once hello creation process completes, click hello tile for hello cluster from hello Startboard toolaunch hello cluster blade.</span></span> <span data-ttu-id="e892e-196">hello 叢集刀鋒視窗會提供下列資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="e892e-196">hello cluster blade provides hello following information.</span></span>
    
    <span data-ttu-id="e892e-197">![叢集刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "叢集屬性")</span><span class="sxs-lookup"><span data-stu-id="e892e-197">![Cluster blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Cluster properties")</span></span>
    
    <span data-ttu-id="e892e-198">使用下列 toounderstand hello 圖示在 hello 這個刀鋒視窗頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="e892e-198">Use hello following toounderstand hello icons at hello top of this blade.</span></span>
    
    * <span data-ttu-id="e892e-199">**概觀**索引標籤會提供有關 hello 叢集例如 hello 名稱、 其所屬 hello 位置，hello 作業系統中，URL hello 叢集儀表板等 hello 資源群組的 hello 基本資訊。</span><span class="sxs-lookup"><span data-stu-id="e892e-199">**Overview** tab provides all hello essential information about hello cluster such as hello name, hello resource group it belongs to, hello location, hello operating system, URL for hello cluster dashboard, etc.</span></span>
    * <span data-ttu-id="e892e-200">**儀表板**會將您導向 toohello Ambari 入口網站與 hello 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="e892e-200">**Dashboard** directs you toohello Ambari portal associated with hello cluster.</span></span>
    * <span data-ttu-id="e892e-201">**安全殼層**： 需要使用 SSH tooaccess hello 叢集的資訊。</span><span class="sxs-lookup"><span data-stu-id="e892e-201">**Secure Shell**: Information needed tooaccess hello cluster using SSH.</span></span>
    * <span data-ttu-id="e892e-202">**延展叢集**可讓您增加 hello 與 hello 叢集相關聯的背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="e892e-202">**Scale cluster** lets you increase hello number of worker nodes associated with hello cluster.</span></span>
    * <span data-ttu-id="e892e-203">**刪除**： 刪除 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e892e-203">**Delete**: Deletes hello HDInsight cluster.</span></span>
    

## <a name="customize-clusters"></a><span data-ttu-id="e892e-204">自訂叢集</span><span class="sxs-lookup"><span data-stu-id="e892e-204">Customize clusters</span></span>
* <span data-ttu-id="e892e-205">請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-205">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>
* <span data-ttu-id="e892e-206">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e892e-206">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="e892e-207">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="e892e-207">Delete hello cluster</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="e892e-208">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e892e-208">Troubleshoot</span></span>

<span data-ttu-id="e892e-209">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="e892e-209">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e892e-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e892e-210">Next steps</span></span>
<span data-ttu-id="e892e-211">既然您已成功建立的 HDInsight 叢集，請使用 hello 如何遵循 toolearn toowork 與您的叢集：</span><span class="sxs-lookup"><span data-stu-id="e892e-211">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="e892e-212">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e892e-212">Hadoop clusters</span></span>
* [<span data-ttu-id="e892e-213">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="e892e-213">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e892e-214">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="e892e-214">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e892e-215">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="e892e-215">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="e892e-216">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="e892e-216">HBase clusters</span></span>
* [<span data-ttu-id="e892e-217">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="e892e-217">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="e892e-218">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="e892e-218">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="e892e-219">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="e892e-219">Storm clusters</span></span>
* [<span data-ttu-id="e892e-220">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="e892e-220">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="e892e-221">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="e892e-221">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="e892e-222">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="e892e-222">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="e892e-223">Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="e892e-223">Spark clusters</span></span>
* [<span data-ttu-id="e892e-224">使用 Scala 來建立獨立的應用程式</span><span class="sxs-lookup"><span data-stu-id="e892e-224">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e892e-225">利用 Livy 在 Spark 叢集上遠端執行工作</span><span class="sxs-lookup"><span data-stu-id="e892e-225">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="e892e-226">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="e892e-226">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e892e-227">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="e892e-227">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e892e-228">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="e892e-228">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

