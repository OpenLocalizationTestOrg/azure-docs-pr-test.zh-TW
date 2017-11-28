---
title: "使用網頁瀏覽器建立 Hadoop 叢集 - Azure HDInsight | Microsoft Docs"
description: "了解如何在 Linux 上使用網頁瀏覽器及 Azure Preview 入口網站，為 HDInsight 建立 Hadoop、HBase、Storm 或 Spark 叢集。"
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
ms.openlocfilehash: d002e362cda2f0ca991b2a13d41c01c13929cdba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-the-azure-portal"></a><span data-ttu-id="2ab44-103">在 HDInsight 中使用 Azure 入口網站建立以 Linux 為基礎的叢集</span><span class="sxs-lookup"><span data-stu-id="2ab44-103">Create Linux-based clusters in HDInsight using the Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="2ab44-104">Azure 入口網站是 Web 架構的管理工具，可用來管理裝載於 Microsoft Azure 雲端中的服務和資源。</span><span class="sxs-lookup"><span data-stu-id="2ab44-104">The Azure portal is a web-based management tool for services and resources hosted in the Microsoft Azure cloud.</span></span> <span data-ttu-id="2ab44-105">在本文中，您將會了解如何使用入口網站來建立以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="2ab44-105">In this article you will learn how to create Linux-based HDInsight clusters using the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ab44-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="2ab44-106">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="2ab44-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="2ab44-107">**An Azure subscription**.</span></span> <span data-ttu-id="2ab44-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="2ab44-109">**現代 Web 瀏覽器**。</span><span class="sxs-lookup"><span data-stu-id="2ab44-109">**A modern web browser**.</span></span> <span data-ttu-id="2ab44-110">Azure 入口網站會使用 HTML5 和 Javascript，而且可能無法在舊版 Web 瀏覽器中正確運作。</span><span class="sxs-lookup"><span data-stu-id="2ab44-110">The Azure  portal uses HTML5 and Javascript, and may not function correctly in older web browsers.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="2ab44-111">建立叢集</span><span class="sxs-lookup"><span data-stu-id="2ab44-111">Create clusters</span></span>
<span data-ttu-id="2ab44-112">Azure 入口網站會公開大部分的叢集屬性。</span><span class="sxs-lookup"><span data-stu-id="2ab44-112">The Azure portal exposes most of the cluster properties.</span></span> <span data-ttu-id="2ab44-113">使用 Azure Resource Manager 範本，您可以隱藏許多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2ab44-113">Using Azure Resource Manager template, you can hide a lot of details.</span></span> <span data-ttu-id="2ab44-114">如需詳細資訊，請參閱 [使用 Azure Resource Manager 範本在 HDInsight 中建立 Linux 型的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-114">For more information, see [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. <span data-ttu-id="2ab44-115">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-115">Sign in to the [Azure  portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2ab44-116">依序按一下 [+]、[智慧 + 分析] 及 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="2ab44-116">Click **+**, click **Intelligence + Analytics**, and then click **HDInsight**.</span></span>
   
    <span data-ttu-id="2ab44-117">![在 Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "在 Azure 入口網站中建立新的叢集")</span><span class="sxs-lookup"><span data-stu-id="2ab44-117">![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "Creating a new cluster in the Azure portal")</span></span>

3. <span data-ttu-id="2ab44-118">在 [HDInsight] 刀鋒視窗中，依序按一下 [自訂 (大小、設定、應用程式)] 和 [基本]，然後輸入下列資訊。</span><span class="sxs-lookup"><span data-stu-id="2ab44-118">In the **HDInsight** blade, click **Custom (size, settings, apps)**, click **Basics**, and then enter the following information.</span></span>

    <span data-ttu-id="2ab44-119">![在 Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "在 Azure 入口網站中建立新的叢集")</span><span class="sxs-lookup"><span data-stu-id="2ab44-119">![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "Creating a new cluster in the Azure portal")</span></span>

    * <span data-ttu-id="2ab44-120">輸入 **叢集名稱**：此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="2ab44-120">Enter **Cluster Name**: This name must be globally unique.</span></span>

    * <span data-ttu-id="2ab44-121">從 [訂用帳戶] 下拉式清單中，選取將用於此叢集的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ab44-121">From the **Subscription** drop-down, select the Azure subscription that will be used for the cluster.</span></span>

    * <span data-ttu-id="2ab44-122">按一下 [叢集類型]，然後選取：</span><span class="sxs-lookup"><span data-stu-id="2ab44-122">Click **Cluster type**, and then select:</span></span>
   
        * <span data-ttu-id="2ab44-123">**叢集類型**︰如果您不知道要選擇哪一個項目，請選取 [Hadoop]。</span><span class="sxs-lookup"><span data-stu-id="2ab44-123">**Cluster Type**: If you don't know what to choose, select **Hadoop**.</span></span> <span data-ttu-id="2ab44-124">它是最受歡迎的叢集類型。</span><span class="sxs-lookup"><span data-stu-id="2ab44-124">It is the most popular cluster type.</span></span>
     
            > [!IMPORTANT]
            > <span data-ttu-id="2ab44-125">HDInsight 叢集有各種不同類型，這些類型各自對應到叢集微調時所針對的工作負載或技術。</span><span class="sxs-lookup"><span data-stu-id="2ab44-125">HDInsight clusters come in a variety of types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="2ab44-126">沒有任何支援方法可建立結合多個類型的叢集，例如在一個叢集上並存 Storm 和 HBase。</span><span class="sxs-lookup"><span data-stu-id="2ab44-126">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span> 
            > 
            > 
        
        * <span data-ttu-id="2ab44-127">**作業系統**：選取 [Linux]。</span><span class="sxs-lookup"><span data-stu-id="2ab44-127">**Operating System**: Select **Linux**.</span></span>
        
        * <span data-ttu-id="2ab44-128">**版本**︰ 如果您不知道要選擇哪一個項目，請使用預設版本。</span><span class="sxs-lookup"><span data-stu-id="2ab44-128">**Version**: Use the default version if you don't know what to choose.</span></span> <span data-ttu-id="2ab44-129">如需詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-129">For more information, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
        * <span data-ttu-id="2ab44-130">**叢集層**：Azure HDInsight 提供兩種類型的巨量資料雲端提供項目：標準層和進階層。</span><span class="sxs-lookup"><span data-stu-id="2ab44-130">**Cluster Tier**: Azure HDInsight provides the big data cloud offerings in two categories: Standard tier and Premium tier.</span></span> <span data-ttu-id="2ab44-131">如需詳細資訊，請參閱 [叢集層](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-131">For more information, see [Cluster tiers](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).</span></span>

    * <span data-ttu-id="2ab44-132">針對 [叢集登入使用者名稱] 和 [叢集登入密碼]，提供管理員使用者的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2ab44-132">For **Cluster login username** and **Cluster login password**, provide the username and password for the admin user.</span></span>

    * <span data-ttu-id="2ab44-133">輸入 **SSH 使用者名稱**，此外，如果您想要讓 SSH 密碼與您先前指定的管理員密碼相同，請選取 [使用與叢集登入相同的密碼] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2ab44-133">Enter an **SSH Username** and if you want to have the SSH password same as the admin password you specified earlier, select the **Use same password as cluster login** check box.</span></span> <span data-ttu-id="2ab44-134">如果不要，請提供**密碼**或**公開金鑰**，這將用來驗證 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="2ab44-134">If not, provide either a **PASSWORD** or **PUBLIC KEY**, which will be used to authenticate the SSH user.</span></span> <span data-ttu-id="2ab44-135">建議使用公開金鑰的方法。</span><span class="sxs-lookup"><span data-stu-id="2ab44-135">Using a public key is the recommended approach.</span></span> <span data-ttu-id="2ab44-136">按一下底部的 [選取]  以儲存認證組態。</span><span class="sxs-lookup"><span data-stu-id="2ab44-136">Click **Select** at the bottom to save the credentials configuration.</span></span>
   
        <span data-ttu-id="2ab44-137">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-137">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    * <span data-ttu-id="2ab44-138">針對 [資源群組]，指定您是否要建立新的資源群組，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2ab44-138">For **Resource group**, specify whether you want to create a new resource group or use an existing one.</span></span>

    * <span data-ttu-id="2ab44-139">指定將建立叢集的資料中心**位置**。</span><span class="sxs-lookup"><span data-stu-id="2ab44-139">Specify a data center **location** where the cluster will be created.</span></span>

    * <span data-ttu-id="2ab44-140">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2ab44-140">Click **Next**.</span></span>

4. <span data-ttu-id="2ab44-141">在 [儲存體] 刀鋒視窗中，指定您要 Azure 儲存體 (WASB) 或 Data Lake Store 做為您的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="2ab44-141">On the **Storage** blade, specify whether you want Azure Storage (WASB) or Data Lake Store as your default storage.</span></span> <span data-ttu-id="2ab44-142">如需詳細資訊，請參閱下表。</span><span class="sxs-lookup"><span data-stu-id="2ab44-142">Look at the table below for more information.</span></span>

    <span data-ttu-id="2ab44-143">![在 Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "在 Azure 入口網站中建立新的叢集")</span><span class="sxs-lookup"><span data-stu-id="2ab44-143">![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "Creating a new cluster in the Azure portal")</span></span>

    | <span data-ttu-id="2ab44-144">儲存體</span><span class="sxs-lookup"><span data-stu-id="2ab44-144">Storage</span></span>                                      | <span data-ttu-id="2ab44-145">說明</span><span class="sxs-lookup"><span data-stu-id="2ab44-145">Description</span></span> |
    |----------------------------------------------|-------------|
    | <span data-ttu-id="2ab44-146">**Azure 儲存體 Blob 做為預設儲存體**</span><span class="sxs-lookup"><span data-stu-id="2ab44-146">**Azure Storage Blobs as default storage**</span></span>   | <ul><li><span data-ttu-id="2ab44-147">對於 [主要儲存體類型]，請選取 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="2ab44-147">For **Primary Storage type**, select **Azure Storage**.</span></span> <span data-ttu-id="2ab44-148">接下來，針對 [選取方法]，如果想要指定屬於您 Azure 訂用帳戶的儲存體帳戶，您可以選擇 [我的訂用帳戶]，然後選取該儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ab44-148">After that, for **Selection method**, you can choose **My subscriptions** if you want to specify a storage account that is part of your Azure subscription and then select the storage account.</span></span> <span data-ttu-id="2ab44-149">否則，按一下 [存取金鑰]，然後提供您希望從您的 Azure 訂用帳戶以外選擇之儲存體帳戶的資訊。</span><span class="sxs-lookup"><span data-stu-id="2ab44-149">Otherwise, click **Access key** and provide the information for the storage account that you want to choose from outside your Azure subscription.</span></span></li><li><span data-ttu-id="2ab44-150">針對 [預設容器]，您可以選擇使用入口網站建議的預設容器名稱，或者自行指定名稱。</span><span class="sxs-lookup"><span data-stu-id="2ab44-150">For **Default container**, you can choose to go with the default container name suggested by the portal or specify your own.</span></span></li><li><span data-ttu-id="2ab44-151">如果您想要使用 WASB 做為預設儲存體，可以(選擇性地) 按一下 [其他儲存體帳戶]，來指定與該叢集相關聯的其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ab44-151">If you are using WASB as default storage, you can (optionally) click **Additional Storage Accounts** to specify additional storage accounts to associate with the cluster.</span></span> <span data-ttu-id="2ab44-152">在 [Azure 儲存體金鑰] 刀鋒視窗中，按一下 [新增儲存體金鑰]，然後可以提供來自您的 Azure 訂用帳戶或其他訂用帳戶的儲存體帳戶 (藉由提供儲存體帳戶存取金鑰)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-152">In the **Azure Storage Keys** blade, click **Add a storage key**, and then you can provide a storage account from your Azure subscriptions or from other subscriptions (by providing the storage account access key).</span></span></li><li><span data-ttu-id="2ab44-153">如果您使用 WASB 做為預設儲存體，您可以 (選擇性地) 按一下 [Data Lake Store 存取]，以指定 Azure Data Lake Store 做為額外的儲存體。</span><span class="sxs-lookup"><span data-stu-id="2ab44-153">If you are using WASB as default storage, you can (optionally) click **Data Lake Store access** to specify Azure Data Lake Store as additional storage.</span></span> <span data-ttu-id="2ab44-154">如需詳細資訊，請參閱[使用 Azure 入口網站建立具有 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-154">For more information, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span></li></ul> |
    | <span data-ttu-id="2ab44-155">**Azure Data Lake Store 做為預設儲存體**</span><span class="sxs-lookup"><span data-stu-id="2ab44-155">**Azure Data Lake Store as default storage**</span></span> | <span data-ttu-id="2ab44-156">針對 [主要儲存體類型]，請選取 [Data Lake Store]，然後參閱[使用 Azure 入口網站建立 HDInsight 叢集與資料湖存放區](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)一文，以取得相關指示。</span><span class="sxs-lookup"><span data-stu-id="2ab44-156">For **Primary storage type**, select **Data Lake Store** and then refer to the article [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) for instructions.</span></span> |
    | <span data-ttu-id="2ab44-157">**外部中繼存放區**</span><span class="sxs-lookup"><span data-stu-id="2ab44-157">**External metastores**</span></span>                      | <span data-ttu-id="2ab44-158">您可以選擇性地指定 SQL 資料庫，來儲存與該叢集相關聯的 Hive 和 Oozie 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2ab44-158">Optionally, you can specify a SQL database to save Hive and Oozie metadata associated with the cluster.</span></span> <span data-ttu-id="2ab44-159">針對 [為 Hive 選取 SQL 資料庫]，選取 SQL 資料庫，然後提供該資料庫的使用者名稱/密碼。</span><span class="sxs-lookup"><span data-stu-id="2ab44-159">For **Select a SQL database for Hive** select a SQL database, and then provide the username/password for the database.</span></span> <span data-ttu-id="2ab44-160">對 Oozie 中繼資料重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2ab44-160">Repeat these steps for Oozie metadata.</span></span><br><br><span data-ttu-id="2ab44-161">針對中繼存放區使用 Azure SQL 資料庫時的一些考量。</span><span class="sxs-lookup"><span data-stu-id="2ab44-161">Some considerations while using Azure SQL database for metastores.</span></span> <ul><li><span data-ttu-id="2ab44-162">用於 metastore 的 Azure SQL Database 必須能夠連線至其他 Azure 服務 (包括 Azure HDInsight)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-162">The Azure SQL database used for the metastore must allow connectivity to other Azure services, including Azure HDInsight.</span></span> <span data-ttu-id="2ab44-163">在 Azure SQL Database 儀表板中，按一下右側的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="2ab44-163">On the Azure SQL database dashboard, on the right side, click the server name.</span></span> <span data-ttu-id="2ab44-164">這是指執行 SQL Database 執行個體的伺服器。</span><span class="sxs-lookup"><span data-stu-id="2ab44-164">This is the server on which the SQL database instance is running.</span></span> <span data-ttu-id="2ab44-165">一旦進入伺服器檢視後，按一下 [設定]，然後在 [Azure 服務] 按一下 [是]，再按 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="2ab44-165">Once you are on the server view, click **Configure**, and then for **Azure Services**, click **Yes**, and then click **Save**.</span></span></li><li><span data-ttu-id="2ab44-166">在建立中繼存放區時，請勿使用包含破折號或連字號的資料庫名稱，因為這會導致叢集建立程序失敗。</span><span class="sxs-lookup"><span data-stu-id="2ab44-166">When creating a metastore, do not use a database name that contains dashes or hyphens, as this can cause the cluster creation process to fail.</span></span></li></ul>                                                                                                                                                                       |

    <span data-ttu-id="2ab44-167">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2ab44-167">Click **Next**.</span></span> 

    > [!WARNING]
    > <span data-ttu-id="2ab44-168">不支援在與 HDInsight 叢集不同的位置中使用其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ab44-168">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

5. <span data-ttu-id="2ab44-169">選擇性地按一下 [應用程式]，以安裝要使用 HDInsight 叢集的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ab44-169">Optionally, click **Applications** to install applications that work with HDInsight clusters.</span></span> <span data-ttu-id="2ab44-170">Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ab44-170">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="2ab44-171">如需詳細資訊，請參閱[安裝 HDInsight 應用程式](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-171">For more information, see [Install HDInsight applications](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).</span></span>


6. <span data-ttu-id="2ab44-172">按一下 [叢集大小]，以顯示將針對此叢集建立的節點相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2ab44-172">Click **Cluster size** to display information about the nodes that will be created for this cluster.</span></span> <span data-ttu-id="2ab44-173">設定該叢集所需的背景工作角色節點數目。</span><span class="sxs-lookup"><span data-stu-id="2ab44-173">Set the number of worker nodes that you need for the cluster.</span></span> <span data-ttu-id="2ab44-174">該叢集的預估成本將會顯示在此刀鋒視窗內。</span><span class="sxs-lookup"><span data-stu-id="2ab44-174">The estimated cost of the cluster will be shown within the blade.</span></span>
   
    <span data-ttu-id="2ab44-175">![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "指定叢集節點的數目")</span><span class="sxs-lookup"><span data-stu-id="2ab44-175">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Specify number of cluster nodes")</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2ab44-176">如果您在建立叢集時或在建立後調整叢集時規劃有 32 個以上的背景工作節點，則您必須選取具有至少 8 個核心和 14 GB ram 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="2ab44-176">If you plan on more than 32 worker nodes, either at cluster creation or by scaling the cluster after creation, then you must select a head node size with at least 8 cores and 14GB ram.</span></span>
   > 
   > <span data-ttu-id="2ab44-177">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-177">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   > 
   > 
   
   <span data-ttu-id="2ab44-178">按 [下一步] 以儲存節點定價組態。</span><span class="sxs-lookup"><span data-stu-id="2ab44-178">Click **Next** to save the node pricing configuration.</span></span>

7. <span data-ttu-id="2ab44-179">按一下 [進階設定] 以設定其他選擇性設定，例如，使用**指令碼動作**自訂叢集以安裝自訂元件，或是加入**虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="2ab44-179">Click **Advanced settings** to configure other optional settings such as using **Script Actions** to customize a cluster to install custom components or joining a **Virtual Network**.</span></span> <span data-ttu-id="2ab44-180">如需詳細資訊，請參閱下表。</span><span class="sxs-lookup"><span data-stu-id="2ab44-180">Look at the table below for more information.</span></span>

    <span data-ttu-id="2ab44-181">![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "指定叢集節點的數目")</span><span class="sxs-lookup"><span data-stu-id="2ab44-181">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Specify number of cluster nodes")</span></span>

    | <span data-ttu-id="2ab44-182">選項</span><span class="sxs-lookup"><span data-stu-id="2ab44-182">Option</span></span> | <span data-ttu-id="2ab44-183">說明</span><span class="sxs-lookup"><span data-stu-id="2ab44-183">Description</span></span> |
    |--------|-------------|
    | <span data-ttu-id="2ab44-184">**指令碼動作**</span><span class="sxs-lookup"><span data-stu-id="2ab44-184">**Script Actions**</span></span> | <span data-ttu-id="2ab44-185">如果您想要在叢集建立時使用自訂指令碼來自訂該叢集，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="2ab44-185">Use this option if you want to use a custom script to customize a cluster, as the cluster is being created.</span></span> <span data-ttu-id="2ab44-186">如需指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-186">For more information about script actions, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span> |
    | <span data-ttu-id="2ab44-187">**虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="2ab44-187">**Virtual Network**</span></span> | <span data-ttu-id="2ab44-188">如果您想要將叢集放入虛擬網路，請選取 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="2ab44-188">Select an Azure virtual network and the subnet if you want to place the cluster into a virtual network.</span></span> <span data-ttu-id="2ab44-189">如需搭配虛擬網路使用 HDInsight 的資訊 (包含虛擬網路的特定組態需求)，請參閱 [使用 Azure 虛擬網路延伸 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-189">For information on using HDInsight with a Virtual Network, including specific configuration requirements for the Virtual Network, see [Extend HDInsight capabilities by using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span> |

    <span data-ttu-id="2ab44-190">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2ab44-190">Click **Next**.</span></span>

8. <span data-ttu-id="2ab44-191">在 [摘要] 刀鋒視窗中，確認您先前輸入的資訊，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="2ab44-191">On the **Summary** blade, verify the information you entered earlier and then click **Create**.</span></span>

    <span data-ttu-id="2ab44-192">![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "指定叢集節點的數目")</span><span class="sxs-lookup"><span data-stu-id="2ab44-192">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Specify number of cluster nodes")</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2ab44-193">建立叢集需要一些時間，通常約 15 分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="2ab44-193">It will take some time for the cluster to be created, usually around 15 minutes.</span></span> <span data-ttu-id="2ab44-194">使用 [「開始面板」] 上的磚，或頁面左邊的 [通知]  項目，以檢查佈建進度。</span><span class="sxs-lookup"><span data-stu-id="2ab44-194">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the provisioning process.</span></span>
    > 
    > 
12. <span data-ttu-id="2ab44-195">建立程序完成後，在「開始面板」按一下該叢集磚，以啟動叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2ab44-195">Once the creation process completes, click the tile for the cluster from the Startboard to launch the cluster blade.</span></span> <span data-ttu-id="2ab44-196">叢集刀鋒視窗會提供以下資訊。</span><span class="sxs-lookup"><span data-stu-id="2ab44-196">The cluster blade provides the following information.</span></span>
    
    <span data-ttu-id="2ab44-197">![叢集刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "叢集屬性")</span><span class="sxs-lookup"><span data-stu-id="2ab44-197">![Cluster blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Cluster properties")</span></span>
    
    <span data-ttu-id="2ab44-198">使用下列資訊來了解此刀鋒視窗頂端的圖示。</span><span class="sxs-lookup"><span data-stu-id="2ab44-198">Use the following to understand the icons at the top of this blade.</span></span>
    
    * <span data-ttu-id="2ab44-199">[概觀] 索引標籤提供關於叢集的所有基本資訊，例如名稱、其所屬的資源群組、位置、作業系統、叢集儀表板 URL 等。</span><span class="sxs-lookup"><span data-stu-id="2ab44-199">**Overview** tab provides all the essential information about the cluster such as the name, the resource group it belongs to, the location, the operating system, URL for the cluster dashboard, etc.</span></span>
    * <span data-ttu-id="2ab44-200">[儀表板] 會將您導向至與叢集相關聯的 Ambari 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2ab44-200">**Dashboard** directs you to the Ambari portal associated with the cluster.</span></span>
    * <span data-ttu-id="2ab44-201">**安全殼層**：使用 SSH 存取叢集所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="2ab44-201">**Secure Shell**: Information needed to access the cluster using SSH.</span></span>
    * <span data-ttu-id="2ab44-202">[調整叢集] 可讓您增加與叢集相關聯的背景工作節點數目。</span><span class="sxs-lookup"><span data-stu-id="2ab44-202">**Scale cluster** lets you increase the number of worker nodes associated with the cluster.</span></span>
    * <span data-ttu-id="2ab44-203">**刪除**：刪除 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="2ab44-203">**Delete**: Deletes the HDInsight cluster.</span></span>
    

## <a name="customize-clusters"></a><span data-ttu-id="2ab44-204">自訂叢集</span><span class="sxs-lookup"><span data-stu-id="2ab44-204">Customize clusters</span></span>
* <span data-ttu-id="2ab44-205">請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-205">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>
* <span data-ttu-id="2ab44-206">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-206">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="2ab44-207">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="2ab44-207">Delete the cluster</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="2ab44-208">疑難排解</span><span class="sxs-lookup"><span data-stu-id="2ab44-208">Troubleshoot</span></span>

<span data-ttu-id="2ab44-209">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="2ab44-209">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ab44-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ab44-210">Next steps</span></span>
<span data-ttu-id="2ab44-211">既然您已成功建立 HDInsight 叢集，請使用下列內容來了解如何使用您的叢集：</span><span class="sxs-lookup"><span data-stu-id="2ab44-211">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="2ab44-212">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="2ab44-212">Hadoop clusters</span></span>
* [<span data-ttu-id="2ab44-213">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="2ab44-213">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2ab44-214">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="2ab44-214">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2ab44-215">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="2ab44-215">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="2ab44-216">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="2ab44-216">HBase clusters</span></span>
* [<span data-ttu-id="2ab44-217">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="2ab44-217">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="2ab44-218">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="2ab44-218">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="2ab44-219">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="2ab44-219">Storm clusters</span></span>
* [<span data-ttu-id="2ab44-220">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="2ab44-220">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="2ab44-221">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="2ab44-221">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="2ab44-222">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="2ab44-222">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="2ab44-223">Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="2ab44-223">Spark clusters</span></span>
* [<span data-ttu-id="2ab44-224">使用 Scala 來建立獨立的應用程式</span><span class="sxs-lookup"><span data-stu-id="2ab44-224">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2ab44-225">利用 Livy 在 Spark 叢集上遠端執行工作</span><span class="sxs-lookup"><span data-stu-id="2ab44-225">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="2ab44-226">Spark 和 BI：搭配 BI 工具來使用 HDInsight 中的 Spark 以執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="2ab44-226">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2ab44-227">Spark 和機器學習：使用 HDInsight 中的 Spark 來預測食物檢查結果</span><span class="sxs-lookup"><span data-stu-id="2ab44-227">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2ab44-228">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="2ab44-228">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

