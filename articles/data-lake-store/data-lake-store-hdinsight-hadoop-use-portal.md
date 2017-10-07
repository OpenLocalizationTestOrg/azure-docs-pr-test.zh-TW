---
title: "aaaUse hello Azure 入口網站 toocreate Azure HDInsight 叢集與資料湖存放區 |Microsoft 文件"
description: "使用 Azure 入口網站 toocreate hello 和使用 Azure Data Lake Store 的 HDInsight 叢集"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a><span data-ttu-id="8f966-103">使用 Data Lake Store 的 HDInsight 叢集建立使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8f966-103">Create HDInsight clusters with Data Lake Store by using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f966-104">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8f966-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="8f966-105">使用 PowerShell (針對預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="8f966-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="8f966-106">使用 PowerShell (針對額外儲存體)</span><span class="sxs-lookup"><span data-stu-id="8f966-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="8f966-107">使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f966-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="8f966-108">了解如何 toouse hello Azure 入口網站 toocreate HDInsight 叢集的 Azure Data Lake Store 帳戶做為 hello 預設儲存體或額外的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="8f966-108">Learn how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or an additional storage.</span></span> <span data-ttu-id="8f966-109">即使額外的儲存體是選擇性的 HDInsight 叢集，則建議 toostore hello 額外的儲存體帳戶中商務資料。</span><span class="sxs-lookup"><span data-stu-id="8f966-109">Even though additional storage is optional for a HDInsight cluster, it is recommended toostore your business data in hello additional storage accounts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f966-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8f966-110">Prerequisites</span></span>
<span data-ttu-id="8f966-111">開始本教學課程之前，請確定您符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f966-111">Before you begin this tutorial, ensure that you've met hello following requirements:</span></span>

* <span data-ttu-id="8f966-112">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8f966-112">**An Azure subscription**.</span></span> <span data-ttu-id="8f966-113">跳過[取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8f966-113">Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8f966-114">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8f966-114">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="8f966-115">請依照下列指示 hello[使用 hello Azure 入口網站開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8f966-115">Follow hello instructions from [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="8f966-116">您也必須建立根資料夾上 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-116">You must also create a root folder on hello account.</span></span>  <span data-ttu-id="8f966-117">在本教學課程中，會使用名為 __/clusters__ 的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="8f966-117">In this tutorial, a root folder called __/clusters__ is used.</span></span>
* <span data-ttu-id="8f966-118">**Azure Active Directory 服務主體**。</span><span class="sxs-lookup"><span data-stu-id="8f966-118">**An Azure Active Directory service principal**.</span></span> <span data-ttu-id="8f966-119">本教學課程提供如何指示 toocreate Azure Active Directory (Azure AD) 中的服務主體。</span><span class="sxs-lookup"><span data-stu-id="8f966-119">This tutorial provides instructions on how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8f966-120">不過，toocreate 服務主體，您必須是 Azure AD 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="8f966-120">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="8f966-121">如果您是系統管理員，則可以略過這項必要條件，並繼續進行 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="8f966-121">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8f966-122">唯有您是 Azure AD 系統管理員，才可以建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="8f966-122">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="8f966-123">您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="8f966-123">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="8f966-124">此外，hello 服務主體必須以建立憑證時，依照[建立服務主體與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)。</span><span class="sxs-lookup"><span data-stu-id="8f966-124">Also, hello service principal must be created with a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>
    >

## <a name="create-an-hdinsight-cluster"></a><span data-ttu-id="8f966-125">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="8f966-125">Create an HDInsight cluster</span></span>

<span data-ttu-id="8f966-126">本節中，您可以建立 HDInsight 叢集與 hello 預設值為 hello 額外的存放裝置的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-126">In this section, you create a HDInsight cluster with Data Lake Store accounts as hello default or hello additional storage.</span></span> <span data-ttu-id="8f966-127">本文只著重 hello 一部分設定 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-127">This article only focuses hello part of configuring Data Lake Store accounts.</span></span>  <span data-ttu-id="8f966-128">Hello 一般叢集建立資訊和程序，請參閱[在 HDInsight 中的建立 Hadoop 叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="8f966-128">For hello general cluster creation information and procedures, see [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a><span data-ttu-id="8f966-129">建立以 Data Lake Store 做為預設儲存體的叢集</span><span class="sxs-lookup"><span data-stu-id="8f966-129">Create a cluster with Data Lake Store as default storage</span></span>

<span data-ttu-id="8f966-130">**Data Lake Store toocreate HDInsight 叢集與 hello 預設儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="8f966-130">**toocreate a HDInsight cluster with a Data Lake Store as hello default storage account**</span></span>

1. <span data-ttu-id="8f966-131">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8f966-131">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f966-132">請遵循[建立叢集](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters)的 hello 建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="8f966-132">Follow [Create clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) for hello general information on creating HDInsight clusters.</span></span>
3. <span data-ttu-id="8f966-133">在 hello**儲存體**刀鋒視窗下**主要儲存體類型**，選取**Data Lake Store**，然後輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f966-133">On hello **Storage** blade, under **Primary storage type**, select **Data Lake Store**, and then enter hello following information:</span></span>

    <span data-ttu-id="8f966-134">![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "新增服務主體 tooHDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="8f966-134">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Add service principal tooHDInsight cluster")</span></span>

    - <span data-ttu-id="8f966-135">**選取 Data Lake Store 帳戶**： 選取現有的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-135">**Select Data Lake Store account**: Select an existing Data Lake Store account.</span></span> <span data-ttu-id="8f966-136">需要現有的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-136">An existing Data Lake Store account is required.</span></span>  <span data-ttu-id="8f966-137">請參閱[必要條件](#prereuisites)。</span><span class="sxs-lookup"><span data-stu-id="8f966-137">See [Prerequisites](#prereuisites).</span></span>
    - <span data-ttu-id="8f966-138">**根路徑**： 輸入 hello 叢集特定檔案的 toobe 儲存的位置路徑。</span><span class="sxs-lookup"><span data-stu-id="8f966-138">**Root path**: Enter a path where hello cluster-specific files are toobe stored.</span></span> <span data-ttu-id="8f966-139">在 hello 螢幕擷取畫面，這是__/叢集/myhdiadlcluster/__中的 hello __/叢集__資料夾必須存在，且 hello 入口網站建立*myhdicluster*資料夾。</span><span class="sxs-lookup"><span data-stu-id="8f966-139">On hello screenshot, it is __/clusters/myhdiadlcluster/__, in which hello __/clusters__ folder must exist, and hello Portal creates *myhdicluster* folder.</span></span>  <span data-ttu-id="8f966-140">hello *myhdicluster* hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="8f966-140">hello *myhdicluster* is hello cluster name.</span></span>
    - <span data-ttu-id="8f966-141">**資料湖存放區存取**: hello Data Lake Store 帳戶與 HDInsight 叢集之間的存取設定。</span><span class="sxs-lookup"><span data-stu-id="8f966-141">**Data Lake Store access**: Configure access between hello Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="8f966-142">如需指示，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="8f966-142">For instructions, see [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>
    - <span data-ttu-id="8f966-143">**其他儲存體帳戶**: hello 叢集新增 Azure 儲存體帳戶做為額外的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-143">**Additional storage accounts**: Add Azure Storage Accounts as additional storage accounts for hello cluster.</span></span> <span data-ttu-id="8f966-144">tooadd 額外資料湖存放區是由 Data Lake Store 帳戶設定為 hello 主要儲存體類型時，給予更多的 Data Lake Store 帳戶中的資料上的 hello 叢集權限。</span><span class="sxs-lookup"><span data-stu-id="8f966-144">tooadd additional Data Lake Stores is done by giving hello cluster permissions on data in more Data Lake Store accounts while configuring a Data Lake Store account as hello primary storage type.</span></span> <span data-ttu-id="8f966-145">請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="8f966-145">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

4. <span data-ttu-id="8f966-146">在 hello**資料湖存放區存取**，按一下 **選取**中, 所述，然後繼續建立叢集與[建立 Hadoop 叢集 HDInsight 中](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8f966-146">On hello **Data Lake Store access**, click **Select**, and then continue with cluster creation as described in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="8f966-147">建立以 Data Lake Store 做為額外儲存體的叢集</span><span class="sxs-lookup"><span data-stu-id="8f966-147">Create a cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="8f966-148">hello 下列指示建立 HDInsight 叢集的 Azure 儲存體帳戶為 hello 預設儲存體，與做為額外的存放裝置的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-148">hello following instructions create a HDInsight cluster with an Azure Storage account as hello default storage, and a Data Lake Store account as an additional storage.</span></span>
<span data-ttu-id="8f966-149">**Data Lake Store toocreate HDInsight 叢集與 hello 預設儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="8f966-149">**toocreate a HDInsight cluster with a Data Lake Store as hello default storage account**</span></span>

1. <span data-ttu-id="8f966-150">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8f966-150">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f966-151">請遵循[建立叢集](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters)的 hello 建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="8f966-151">Follow [Create clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) for hello general information on creating HDInsight clusters.</span></span>
3. <span data-ttu-id="8f966-152">在 hello**儲存體**刀鋒視窗底下**主要儲存體類型**，選取**Azure 儲存體**，然後輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f966-152">On hello **Storage** blade, under **Primary storage type**, select **Azure Storage**, and then enter hello following information:</span></span>

    <span data-ttu-id="8f966-153">![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "新增服務主體 tooHDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="8f966-153">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Add service principal tooHDInsight cluster")</span></span>

    - <span data-ttu-id="8f966-154">**選取方法**： 使用其中一種 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="8f966-154">**Selection method**: use one of hello following options:</span></span>

        * <span data-ttu-id="8f966-155">toospecify 屬於您 Azure 訂用帳戶的儲存體帳戶選取**我的訂閱**，然後選取 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-155">toospecify a storage account that is part of your Azure subscription, select **My subscriptions**, and then select hello storage account.</span></span>
        * <span data-ttu-id="8f966-156">toospecify 超出您的 Azure 訂閱，選取儲存體帳戶**便捷鍵**，然後提供 hello hello 外部儲存體帳戶的資訊。</span><span class="sxs-lookup"><span data-stu-id="8f966-156">toospecify a storage account that is outside your Azure subscription, select **Access key**, and then provide hello information for hello outside storage account.</span></span>

    - <span data-ttu-id="8f966-157">**預設容器**： 使用任一個 hello 預設值或指定您自己的名稱。</span><span class="sxs-lookup"><span data-stu-id="8f966-157">**Default container**: use either hello default value or specify your own name.</span></span>

    - <span data-ttu-id="8f966-158">其他儲存體帳戶： 將多個 Azure 儲存體帳戶新增為 hello 額外的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="8f966-158">Additional Storage accounts: add more Azure Storage accounts as hello additional storage.</span></span>
    - <span data-ttu-id="8f966-159">資料湖存放區存取： hello Data Lake Store 帳戶與 HDInsight 叢集之間的存取設定。</span><span class="sxs-lookup"><span data-stu-id="8f966-159">Data Lake Store access: configure access between hello Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="8f966-160">如需指示，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="8f966-160">For instructions see [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="8f966-161">設定 Data Lake Store 存取</span><span class="sxs-lookup"><span data-stu-id="8f966-161">Configure Data Lake Store access</span></span> 

<span data-ttu-id="8f966-162">在本節中，您將會使用 Azure Active Directory 服務主體設定 Data Lake Store 與 HDInsight 叢集之間的存取。</span><span class="sxs-lookup"><span data-stu-id="8f966-162">In this section, you configure Data Lake Store access from HDInsight clusters using an Azure Active Directory service principal.</span></span> 

### <a name="specify-a-service-principal"></a><span data-ttu-id="8f966-163">指定服務主體</span><span class="sxs-lookup"><span data-stu-id="8f966-163">Specify a service principal</span></span>

<span data-ttu-id="8f966-164">從 hello Azure 入口網站，您可以使用現有的服務主體或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="8f966-164">From hello Azure portal, you can either use an existing service principal or create a new one.</span></span>

<span data-ttu-id="8f966-165">**toocreate hello Azure 入口網站的服務主體**</span><span class="sxs-lookup"><span data-stu-id="8f966-165">**toocreate a service principal from hello Azure portal**</span></span>

1. <span data-ttu-id="8f966-166">按一下**資料湖存放區存取**的 hello 存放區 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8f966-166">Click **Data Lake Store access** from hello Store blade.</span></span>
2. <span data-ttu-id="8f966-167">在 hello**資料湖存放區存取**刀鋒視窗中，按一下 **建立新**。</span><span class="sxs-lookup"><span data-stu-id="8f966-167">On hello **Data Lake Store access** blade, click **Create new**.</span></span>
3. <span data-ttu-id="8f966-168">按一下**服務主體**，然後依照 hello 指示 toocreate 服務主體。</span><span class="sxs-lookup"><span data-stu-id="8f966-168">Click **Service Principal**, and then follow hello instructions toocreate a service principal.</span></span>
4. <span data-ttu-id="8f966-169">如果您決定 toouse 下載 hello 憑證一次在未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="8f966-169">Download hello certificate if you decide toouse it again in hello future.</span></span> <span data-ttu-id="8f966-170">這是很有用，如果您想 toouse hello 相同服務主體時建立額外的 HDInsight 叢集下載 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="8f966-170">Downloading hello certificate is useful if you want toouse hello same service principal when you create additional HDInsight clusters.</span></span>

    <span data-ttu-id="8f966-171">![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "新增服務主體 tooHDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="8f966-171">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Add service principal tooHDInsight cluster")</span></span>

4. <span data-ttu-id="8f966-172">按一下**存取**tooconfigure hello 資料夾存取。</span><span class="sxs-lookup"><span data-stu-id="8f966-172">Click **Access** tooconfigure hello folder access.</span></span>  <span data-ttu-id="8f966-173">請參閱[設定檔案權限](#configure-file-permissions)。</span><span class="sxs-lookup"><span data-stu-id="8f966-173">See [Configure file permissions](#configure-file-permissions).</span></span>


<span data-ttu-id="8f966-174">**toouse 現有服務主體從 hello Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="8f966-174">**toouse an existing service principal from hello Azure portal**</span></span>

1. <span data-ttu-id="8f966-175">按一下 [Data Lake Store 存取]。</span><span class="sxs-lookup"><span data-stu-id="8f966-175">Click **Data Lake Store access**.</span></span>
1. <span data-ttu-id="8f966-176">在 hello**資料湖存放區存取**刀鋒視窗中，按一下 **使用現有**。</span><span class="sxs-lookup"><span data-stu-id="8f966-176">On hello **Data Lake Store access** blade, click **Use existing**.</span></span>
2. <span data-ttu-id="8f966-177">按一下 [服務主體]，然後選取一個服務主體。</span><span class="sxs-lookup"><span data-stu-id="8f966-177">Click **Service Principal**, and then select a service principal.</span></span> 
3. <span data-ttu-id="8f966-178">上傳您的選取的服務主體相關聯的 hello 憑證 （.pfx 檔案），然後輸入 hello 憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="8f966-178">Upload hello certificate (.pfx file) that's associated with your selected service principal, and then enter hello certificate password.</span></span>

    <span data-ttu-id="8f966-179">![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "新增服務主體 tooHDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="8f966-179">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Add service principal tooHDInsight cluster")</span></span>

4. <span data-ttu-id="8f966-180">按一下**存取**tooconfigure hello 資料夾存取。</span><span class="sxs-lookup"><span data-stu-id="8f966-180">Click **Access** tooconfigure hello folder access.</span></span>  <span data-ttu-id="8f966-181">請參閱[設定檔案權限](#configure-file-permissions)。</span><span class="sxs-lookup"><span data-stu-id="8f966-181">See [Configure file permissions](#configure-file-permissions).</span></span>


### <span data-ttu-id="8f966-182"><a name="configure-file-permissions"></a>設定檔案權限</span><span class="sxs-lookup"><span data-stu-id="8f966-182"><a name="configure-file-permissions"></a>Configure file permissions</span></span>

<span data-ttu-id="8f966-183">hello 設定會根據是否 hello 帳戶會當做 hello 預設儲存體或其他儲存體帳戶而不同：</span><span class="sxs-lookup"><span data-stu-id="8f966-183">hello configures are different depending on whether hello account is used as hello default storage or an additional storage account:</span></span>

- <span data-ttu-id="8f966-184">作為預設儲存體</span><span class="sxs-lookup"><span data-stu-id="8f966-184">Used as default storage</span></span>

    - <span data-ttu-id="8f966-185">在根層級 hello hello Data Lake Store 帳戶的權限</span><span class="sxs-lookup"><span data-stu-id="8f966-185">permission at hello root level of hello Data Lake Store account</span></span>
    - <span data-ttu-id="8f966-186">hello HDInsight 叢集存放裝置 hello 根層級的權限。</span><span class="sxs-lookup"><span data-stu-id="8f966-186">permission at hello root level of hello HDInsight cluster storage.</span></span> <span data-ttu-id="8f966-187">例如，hello __/叢集__hello 教學課程中先前使用的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8f966-187">For example, hello __/clusters__ folder used earlier in hello tutorial.</span></span>
- <span data-ttu-id="8f966-188">作為其他儲存體</span><span class="sxs-lookup"><span data-stu-id="8f966-188">Use as an additional storage</span></span>

    - <span data-ttu-id="8f966-189">在您需要在此檔案存取的 hello 資料夾的權限。</span><span class="sxs-lookup"><span data-stu-id="8f966-189">Permission at hello folders where you need file access.</span></span>

<span data-ttu-id="8f966-190">**在 hello Data Lake Store 帳戶的根層級的 tooassign 權限**</span><span class="sxs-lookup"><span data-stu-id="8f966-190">**tooassign permission at hello Data Lake Store account root level**</span></span>

1. <span data-ttu-id="8f966-191">在 hello**資料湖存放區存取**刀鋒視窗中，按一下 **存取**。</span><span class="sxs-lookup"><span data-stu-id="8f966-191">On hello **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="8f966-192">hello**選取檔案的權限**開啟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8f966-192">hello **Select file permissions** blade is opened.</span></span> <span data-ttu-id="8f966-193">它會列出您的訂用帳戶中的所有 hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-193">It lists all hello Data Lake Store accounts in your subscription.</span></span>
2. <span data-ttu-id="8f966-194">將滑鼠停留 （請勿按一下） hello 的結束滑鼠停留 hello hello toomake hello 可見，核取方塊，然後選取 hello 核取方塊的 Data Lake Store 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="8f966-194">Hover (do not click) hello mouse over hello name of hello Data Lake Store account toomake hello check box visible, then select hello check box.</span></span>

    <span data-ttu-id="8f966-195">![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "新增服務主體 tooHDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="8f966-195">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Add service principal tooHDInsight cluster")</span></span>

  <span data-ttu-id="8f966-196">根據預設，__READ__、__WRITE__ 和 __EXECUTE__ 會全部選取。</span><span class="sxs-lookup"><span data-stu-id="8f966-196">By default, __READ__, __WRITE__, AND __EXECUTE__ are all selected.</span></span>

3. <span data-ttu-id="8f966-197">按一下**選取**上 hello hello 頁面的底部。</span><span class="sxs-lookup"><span data-stu-id="8f966-197">Click **Select** on hello bottom of hello page.</span></span>
4. <span data-ttu-id="8f966-198">按一下**執行**tooassign 權限。</span><span class="sxs-lookup"><span data-stu-id="8f966-198">Click **Run** tooassign permission.</span></span>
5. <span data-ttu-id="8f966-199">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="8f966-199">Click **Done**.</span></span>

<span data-ttu-id="8f966-200">**在 hello HDInsight 叢集根層級的 tooassign 權限**</span><span class="sxs-lookup"><span data-stu-id="8f966-200">**tooassign permission at hello HDInsight cluster root level**</span></span>

1. <span data-ttu-id="8f966-201">在 hello**資料湖存放區存取**刀鋒視窗中，按一下 **存取**。</span><span class="sxs-lookup"><span data-stu-id="8f966-201">On hello **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="8f966-202">hello**選取檔案的權限**開啟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8f966-202">hello **Select file permissions** blade is opened.</span></span> <span data-ttu-id="8f966-203">它會列出您的訂用帳戶中的所有 hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-203">It lists all hello Data Lake Store accounts in your subscription.</span></span>
1. <span data-ttu-id="8f966-204">從 hello**選取檔案的權限**刀鋒視窗中，按一下 hello 資料湖存放區名稱 tooshow 其內容。</span><span class="sxs-lookup"><span data-stu-id="8f966-204">From hello **Select file permissions** blade, click hello Data Lake Store name tooshow its content.</span></span>
2. <span data-ttu-id="8f966-205">選取左側的 hello 資料夾 hello hello 核取方塊來選取 hello HDInsight 叢集儲存區根目錄。</span><span class="sxs-lookup"><span data-stu-id="8f966-205">Select hello HDInsight cluster storage root by selecting hello checkbox on hello left of hello folder.</span></span> <span data-ttu-id="8f966-206">稍早根據 toohello 螢幕擷取畫面，hello 叢集儲存區根目錄是__/叢集__您選取為預設的存放裝置 hello 資料湖存放區時所指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8f966-206">According toohello screenshot earlier, hello cluster storage root is __/clusters__ folder that you specified while selecting hello Data Lake Store as default storage.</span></span>
3. <span data-ttu-id="8f966-207">Hello 資料夾上設定 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="8f966-207">Set hello permissions on hello folder.</span></span>  <span data-ttu-id="8f966-208">根據預設，讀取、寫入和執行會全部選取。</span><span class="sxs-lookup"><span data-stu-id="8f966-208">By default, read, write, and execute are all selected.</span></span>
4. <span data-ttu-id="8f966-209">按一下**選取**上 hello hello 頁面的底部。</span><span class="sxs-lookup"><span data-stu-id="8f966-209">Click **Select** on hello bottom of hello page.</span></span>
5. <span data-ttu-id="8f966-210">按一下 **[執行]**。</span><span class="sxs-lookup"><span data-stu-id="8f966-210">Click **Run**.</span></span>
6. <span data-ttu-id="8f966-211">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="8f966-211">Click **Done**.</span></span>

<span data-ttu-id="8f966-212">如果您使用 Data Lake Store 作為額外的存放裝置，您必須指派只能用於 hello 資料夾的權限的 tooaccess 從 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="8f966-212">If you are using Data Lake Store as additional storage, you must assign permission only for hello folders that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="8f966-213">例如，在 hello 以下螢幕擷取畫面，您提供存取只太**hdiaddonstorage** Data Lake Store 帳戶中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8f966-213">For example, in hello screenshot below, you provide access only too**hdiaddonstorage** folder in a Data Lake Store account.</span></span>

<span data-ttu-id="8f966-214">![指派服務主體的權限 toohello HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "指派服務主體的權限 toohello HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="8f966-214">![Assign service principal permissions toohello HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "Assign service principal permissions toohello HDInsight cluster")</span></span>


## <a name="verify-cluster-set-up"></a><span data-ttu-id="8f966-215">確認叢集設定</span><span class="sxs-lookup"><span data-stu-id="8f966-215">Verify cluster set up</span></span>

<span data-ttu-id="8f966-216">Hello 叢集安裝程式完成之後，在 hello 叢集刀鋒視窗中，確認您的結果執行一個或兩個步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f966-216">After hello cluster setup is complete, on hello cluster blade, verify your results by doing either or both of hello following steps:</span></span>

* <span data-ttu-id="8f966-217">hello hello 叢集為您指定的 hello Data Lake Store 帳戶的相關聯的儲存體，請按一下 tooverify**儲存體帳戶**hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="8f966-217">tooverify that hello associated storage for hello cluster is hello Data Lake Store account that you specified, click **Storage accounts** in hello left pane.</span></span>

    <span data-ttu-id="8f966-218">![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "新增服務主體 tooHDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="8f966-218">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Add service principal tooHDInsight cluster")</span></span>

* <span data-ttu-id="8f966-219">hello 服務主體的 tooverify 是正確與 hello HDInsight 叢集相關聯，請按一下**資料湖存放區存取**hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="8f966-219">tooverify that hello service principal is correctly associated with hello HDInsight cluster, click **Data Lake Store access** in hello left pane.</span></span>

    <span data-ttu-id="8f966-220">![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "新增服務主體 tooHDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="8f966-220">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Add service principal tooHDInsight cluster")</span></span>


## <a name="examples"></a><span data-ttu-id="8f966-221">範例</span><span class="sxs-lookup"><span data-stu-id="8f966-221">Examples</span></span>

<span data-ttu-id="8f966-222">您已將設定 Data Lake Store 的 hello 叢集為您的儲存體之後，請參閱 toothese 範例 toouse HDInsight 叢集 tooanalyze hello 資料儲存在資料湖存放區中的方式。</span><span class="sxs-lookup"><span data-stu-id="8f966-222">After you have set up hello cluster with Data Lake Store as your storage, refer toothese examples of how toouse HDInsight cluster tooanalyze hello data that's stored in Data Lake Store.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a><span data-ttu-id="8f966-223">針對 Data Lake Store (做為主要儲存體) 中的資料執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="8f966-223">Run a Hive query against data in a Data Lake Store (as primary storage)</span></span>

<span data-ttu-id="8f966-224">toorun Hive 查詢，使用 hello Ambari 入口網站中的 hello Hive 檢視介面。</span><span class="sxs-lookup"><span data-stu-id="8f966-224">toorun a Hive query, use hello Hive views interface in hello Ambari portal.</span></span> <span data-ttu-id="8f966-225">如需有關如何檢視 toouse Ambari Hive 的指示，請參閱[使用 hello HDInsight 中的 Hadoop hive 控制檔的檢視](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md)。</span><span class="sxs-lookup"><span data-stu-id="8f966-225">For instructions on how toouse Ambari Hive views, see [Use hello Hive View with Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

<span data-ttu-id="8f966-226">當您使用資料湖存放區中的資料時，有幾個字串 toochange。</span><span class="sxs-lookup"><span data-stu-id="8f966-226">When you work with data in a Data Lake Store, there are a few strings toochange.</span></span>

<span data-ttu-id="8f966-227">如果您使用，例如，資料湖存放區做為主要儲存體，以建立 hello 叢集 hello 路徑 toohello 資料是： *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*。</span><span class="sxs-lookup"><span data-stu-id="8f966-227">If you use, for example, hello cluster that you created with Data Lake Store as primary storage, hello path toohello data is: *adl://<data_lake_store_account_name>/azuredatalakestore.net/path/to/file*.</span></span> <span data-ttu-id="8f966-228">Hive 查詢 toocreate 會儲存在 hello Data Lake Store 帳戶的範例資料中的資料表看起來像 hello 後面的陳述式中：</span><span class="sxs-lookup"><span data-stu-id="8f966-228">A Hive query toocreate a table from sample data that's stored in hello Data Lake Store account looks like hello following statement:</span></span>

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

<span data-ttu-id="8f966-229">說明：</span><span class="sxs-lookup"><span data-stu-id="8f966-229">Descriptions:</span></span>
* <span data-ttu-id="8f966-230">`adl://hdiadlstorage.azuredatalakestore.net/`是 hello 根 hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f966-230">`adl://hdiadlstorage.azuredatalakestore.net/` is hello root of hello Data Lake Store account.</span></span>
* <span data-ttu-id="8f966-231">`/clusters/myhdiadlcluster`是 hello 根 hello 建立 hello 叢集時，您指定的叢集資料。</span><span class="sxs-lookup"><span data-stu-id="8f966-231">`/clusters/myhdiadlcluster` is hello root of hello cluster data that you specified while creating hello cluster.</span></span>
* <span data-ttu-id="8f966-232">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`是您在 hello 查詢中使用的 hello 範例檔案的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="8f966-232">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/` is hello location of hello sample file that you used in hello query.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a><span data-ttu-id="8f966-233">針對 Data Lake Store (做為額外儲存體) 中的資料執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="8f966-233">Run a Hive query against data in a Data Lake Store (as additional storage)</span></span>

<span data-ttu-id="8f966-234">如果您建立的 hello 叢集做為預設儲存體使用 Blob 儲存體，hello 範例資料不會包含在 hello Azure Data Lake Store 帳戶做為額外的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="8f966-234">If hello cluster that you created uses Blob storage as default storage, hello sample data is not contained in hello Azure Data Lake Store account that's used as additional storage.</span></span> <span data-ttu-id="8f966-235">在這種情況下，第一次傳送 hello 資料從 Blob 儲存體 toohello 資料湖存放區，然後再執行 hello 查詢 hello 前面範例所示。</span><span class="sxs-lookup"><span data-stu-id="8f966-235">In such a case, first transfer hello data from Blob storage toohello Data Lake Store, and then run hello queries as shown in hello preceding example.</span></span>

<span data-ttu-id="8f966-236">上如何 toocopy 從 Blob 儲存體 tooa 資料湖存放區資料的資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="8f966-236">For information on how toocopy data from Blob storage tooa Data Lake Store, see hello following articles:</span></span>

* [<span data-ttu-id="8f966-237">使用 Azure 儲存體 blob 與資料湖存放區之間 Distcp toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="8f966-237">Use Distcp toocopy data between Azure Storage blobs and Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
* [<span data-ttu-id="8f966-238">使用 AdlCopy toocopy 資料從 Azure 儲存體 blob tooData 湖存放區</span><span class="sxs-lookup"><span data-stu-id="8f966-238">Use AdlCopy toocopy data from Azure Storage blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a><span data-ttu-id="8f966-239">使用 Data Lake Store 搭配 Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="8f966-239">Use Data Lake Store with a Spark cluster</span></span>
<span data-ttu-id="8f966-240">您可以使用 Spark 叢集 toorun Spark 作業上儲存資料湖存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="8f966-240">You can use a Spark cluster toorun Spark jobs on data that is stored in a Data Lake Store.</span></span> <span data-ttu-id="8f966-241">如需詳細資訊，請參閱[資料湖存放區中的使用 HDInsight Spark 叢集 tooanalyze 資料](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="8f966-241">For more information, see [Use HDInsight Spark cluster tooanalyze data in Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).</span></span>


### <a name="use-data-lake-store-in-a-storm-topology"></a><span data-ttu-id="8f966-242">在 Storm 拓撲中使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8f966-242">Use Data Lake Store in a Storm topology</span></span>
<span data-ttu-id="8f966-243">您可以使用 Storm 拓撲 hello Data Lake Store toowrite 資料。</span><span class="sxs-lookup"><span data-stu-id="8f966-243">You can use hello Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="8f966-244">如需有關指示 tooachieve 此案例中，請參閱[與 HDInsight Apache Storm 與使用 Azure Data Lake Store](../hdinsight/hdinsight-storm-write-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="8f966-244">For instructions on how tooachieve this scenario, see [Use Azure Data Lake Store with Apache Storm with HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8f966-245">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8f966-245">See also</span></span>
* [<span data-ttu-id="8f966-246">PowerShell： 建立 HDInsight 叢集 toouse 資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="8f966-246">PowerShell: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
