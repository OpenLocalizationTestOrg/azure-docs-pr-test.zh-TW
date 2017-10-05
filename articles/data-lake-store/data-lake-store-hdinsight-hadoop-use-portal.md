---
title: "使用 Azure 入口網站建立搭配 Data Lake Store 運作的 HDInsight Hadoop 叢集 | Microsoft Docs"
description: "使用 Azure 入口網站建立和使用搭配 Azure Data Lake Store 運作的 HDInsight Hadoop 叢集"
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
ms.openlocfilehash: 9dd56efb89e07ea61ae431d1ea2accd721cd6502
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-the-azure-portal"></a><span data-ttu-id="935bd-103">使用 Azure 入口網站建立搭配 Data Lake Store 的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="935bd-103">Create HDInsight clusters with Data Lake Store by using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="935bd-104">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="935bd-104">Use the Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="935bd-105">使用 PowerShell (針對預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="935bd-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="935bd-106">使用 PowerShell (針對額外儲存體)</span><span class="sxs-lookup"><span data-stu-id="935bd-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="935bd-107">使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="935bd-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="935bd-108">了解如何利用 Azure 入口網站，建立使用 Azure Data Lake Store 帳戶作為預設儲存體或其他儲存體的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="935bd-108">Learn how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or an additional storage.</span></span> <span data-ttu-id="935bd-109">即使其他儲存體是 HDInsight 叢集的選用項目，還是建議將您的商務資料儲存在其他儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="935bd-109">Even though additional storage is optional for a HDInsight cluster, it is recommended to store your business data in the additional storage accounts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="935bd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="935bd-110">Prerequisites</span></span>
<span data-ttu-id="935bd-111">開始本教學課程之前，確保您已符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="935bd-111">Before you begin this tutorial, ensure that you've met the following requirements:</span></span>

* <span data-ttu-id="935bd-112">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="935bd-112">**An Azure subscription**.</span></span> <span data-ttu-id="935bd-113">請移至[取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="935bd-113">Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="935bd-114">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="935bd-114">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="935bd-115">遵循[使用 Azure 入口網站開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md) 的指示操作。</span><span class="sxs-lookup"><span data-stu-id="935bd-115">Follow the instructions from [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="935bd-116">您也必須在此帳戶上建立根資料夾。</span><span class="sxs-lookup"><span data-stu-id="935bd-116">You must also create a root folder on the account.</span></span>  <span data-ttu-id="935bd-117">在本教學課程中，會使用名為 __/clusters__ 的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="935bd-117">In this tutorial, a root folder called __/clusters__ is used.</span></span>
* <span data-ttu-id="935bd-118">**Azure Active Directory 服務主體**。</span><span class="sxs-lookup"><span data-stu-id="935bd-118">**An Azure Active Directory service principal**.</span></span> <span data-ttu-id="935bd-119">本教學課程提供有關如何在 Azure Active Directory (Azure AD) 中建立服務主體的指示。</span><span class="sxs-lookup"><span data-stu-id="935bd-119">This tutorial provides instructions on how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="935bd-120">不過，您必須是 Azure AD 系統管理員，才能建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="935bd-120">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="935bd-121">如果您是系統管理員，就可以略過這項先決條件並繼續進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="935bd-121">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="935bd-122">唯有您是 Azure AD 系統管理員，才可以建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="935bd-122">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="935bd-123">您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="935bd-123">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="935bd-124">此外，必須使用憑證來建立服務主體，如[使用憑證來建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)所述。</span><span class="sxs-lookup"><span data-stu-id="935bd-124">Also, the service principal must be created with a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>
    >

## <a name="create-an-hdinsight-cluster"></a><span data-ttu-id="935bd-125">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="935bd-125">Create an HDInsight cluster</span></span>

<span data-ttu-id="935bd-126">在本節中，您會建立一個使用 Data Lake Store 帳戶作為預設或其他儲存體的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="935bd-126">In this section, you create a HDInsight cluster with Data Lake Store accounts as the default or the additional storage.</span></span> <span data-ttu-id="935bd-127">本文僅著重於設定 Data Lake Store 帳戶的部分。</span><span class="sxs-lookup"><span data-stu-id="935bd-127">This article only focuses the part of configuring Data Lake Store accounts.</span></span>  <span data-ttu-id="935bd-128">如需一般叢集建立資訊和程序，請參閱 [在 HDInsight 中建立 Hadoop 叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="935bd-128">For the general cluster creation information and procedures, see [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a><span data-ttu-id="935bd-129">建立以 Data Lake Store 做為預設儲存體的叢集</span><span class="sxs-lookup"><span data-stu-id="935bd-129">Create a cluster with Data Lake Store as default storage</span></span>

<span data-ttu-id="935bd-130">**建立使用 Data Lake Store 作為預設儲存體帳戶的 HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="935bd-130">**To create a HDInsight cluster with a Data Lake Store as the default storage account**</span></span>

1. <span data-ttu-id="935bd-131">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="935bd-131">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="935bd-132">請遵循[建立叢集](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters)，以取得建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="935bd-132">Follow [Create clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) for the general information on creating HDInsight clusters.</span></span>
3. <span data-ttu-id="935bd-133">在 [儲存體] 刀鋒視窗的 [主要儲存體類型] 下，選取 [Data Lake Store]，然後輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="935bd-133">On the **Storage** blade, under **Primary storage type**, select **Data Lake Store**, and then enter the following information:</span></span>

    <span data-ttu-id="935bd-134">![將服務主體新增至 HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "將服務主體新增至 HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="935bd-134">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Add service principal to HDInsight cluster")</span></span>

    - <span data-ttu-id="935bd-135">**選取 Data Lake Store 帳戶**： 選取現有的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="935bd-135">**Select Data Lake Store account**: Select an existing Data Lake Store account.</span></span> <span data-ttu-id="935bd-136">需要現有的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="935bd-136">An existing Data Lake Store account is required.</span></span>  <span data-ttu-id="935bd-137">請參閱[必要條件](#prereuisites)。</span><span class="sxs-lookup"><span data-stu-id="935bd-137">See [Prerequisites](#prereuisites).</span></span>
    - <span data-ttu-id="935bd-138">**根路徑**：輸入要儲存叢集特定檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="935bd-138">**Root path**: Enter a path where the cluster-specific files are to be stored.</span></span> <span data-ttu-id="935bd-139">在螢幕擷取畫面上，它是 __/clusters/myhdiadlcluster/__，其中 __/clusters__ 資料夾必須已存在，而入口網站會建立 *myhdicluster* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="935bd-139">On the screenshot, it is __/clusters/myhdiadlcluster/__, in which the __/clusters__ folder must exist, and the Portal creates *myhdicluster* folder.</span></span>  <span data-ttu-id="935bd-140">*myhdicluster* 是叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="935bd-140">The *myhdicluster* is the cluster name.</span></span>
    - <span data-ttu-id="935bd-141">**Data Lake Store 存取**：設定 Data Lake Store 帳戶與 HDInsight 叢集之間的存取。</span><span class="sxs-lookup"><span data-stu-id="935bd-141">**Data Lake Store access**: Configure access between the Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="935bd-142">如需指示，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="935bd-142">For instructions, see [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>
    - <span data-ttu-id="935bd-143">**其他儲存體帳戶**：新增 Azure 儲存體帳戶作為叢集的其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="935bd-143">**Additional storage accounts**: Add Azure Storage Accounts as additional storage accounts for the cluster.</span></span> <span data-ttu-id="935bd-144">若要新增其他 Data Lake Store，做法是設定某個 Data Lake Store 帳戶作為主要儲存體類型，同時授與叢集存取其他 Data Lake Store 帳戶資料的權限。</span><span class="sxs-lookup"><span data-stu-id="935bd-144">To add additional Data Lake Stores is done by giving the cluster permissions on data in more Data Lake Store accounts while configuring a Data Lake Store account as the primary storage type.</span></span> <span data-ttu-id="935bd-145">請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="935bd-145">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

4. <span data-ttu-id="935bd-146">在 [Data Lake Store 存取權] 上按一下 [選取]，然後繼續進行叢集建立作業，如[在 HDInsight 中建立 Hadoop 叢集](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md)所述。</span><span class="sxs-lookup"><span data-stu-id="935bd-146">On the **Data Lake Store access**, click **Select**, and then continue with cluster creation as described in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="935bd-147">建立以 Data Lake Store 做為額外儲存體的叢集</span><span class="sxs-lookup"><span data-stu-id="935bd-147">Create a cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="935bd-148">下列指示說明如何建立使用 Azure 儲存體帳戶作為預設儲存體，並使用 Data Lake Store 帳戶作為其他儲存體的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="935bd-148">The following instructions create a HDInsight cluster with an Azure Storage account as the default storage, and a Data Lake Store account as an additional storage.</span></span>
<span data-ttu-id="935bd-149">**建立使用 Data Lake Store 作為預設儲存體帳戶的 HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="935bd-149">**To create a HDInsight cluster with a Data Lake Store as the default storage account**</span></span>

1. <span data-ttu-id="935bd-150">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="935bd-150">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="935bd-151">請遵循[建立叢集](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters)，以取得建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="935bd-151">Follow [Create clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) for the general information on creating HDInsight clusters.</span></span>
3. <span data-ttu-id="935bd-152">在 [儲存體] 刀鋒視窗的 [主要儲存體類型] 下，選取 [Azure 儲存體]，然後輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="935bd-152">On the **Storage** blade, under **Primary storage type**, select **Azure Storage**, and then enter the following information:</span></span>

    <span data-ttu-id="935bd-153">![將服務主體新增至 HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "將服務主體新增至 HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="935bd-153">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Add service principal to HDInsight cluster")</span></span>

    - <span data-ttu-id="935bd-154">**選取方法**：使用下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="935bd-154">**Selection method**: use one of the following options:</span></span>

        * <span data-ttu-id="935bd-155">若要指定屬於 Azure 訂用帳戶的儲存體帳戶，請選取 [我的訂用帳戶]，然後選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="935bd-155">To specify a storage account that is part of your Azure subscription, select **My subscriptions**, and then select the storage account.</span></span>
        * <span data-ttu-id="935bd-156">若要指定 Azure 訂用帳戶外部的儲存體帳戶，請選取 [存取金鑰]，然後提供外部儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="935bd-156">To specify a storage account that is outside your Azure subscription, select **Access key**, and then provide the information for the outside storage account.</span></span>

    - <span data-ttu-id="935bd-157">**預設容器**：使用預設值或指定您自己的名稱。</span><span class="sxs-lookup"><span data-stu-id="935bd-157">**Default container**: use either the default value or specify your own name.</span></span>

    - <span data-ttu-id="935bd-158">其他儲存體帳戶：新增其他 Azure 儲存體帳戶作為其他儲存體。</span><span class="sxs-lookup"><span data-stu-id="935bd-158">Additional Storage accounts: add more Azure Storage accounts as the additional storage.</span></span>
    - <span data-ttu-id="935bd-159">Data Lake Store 存取：設定 Data Lake Store 帳戶與 HDInsight 叢集之間的存取。</span><span class="sxs-lookup"><span data-stu-id="935bd-159">Data Lake Store access: configure access between the Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="935bd-160">如需指示，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="935bd-160">For instructions see [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="935bd-161">設定 Data Lake Store 存取</span><span class="sxs-lookup"><span data-stu-id="935bd-161">Configure Data Lake Store access</span></span> 

<span data-ttu-id="935bd-162">在本節中，您將會使用 Azure Active Directory 服務主體設定 Data Lake Store 與 HDInsight 叢集之間的存取。</span><span class="sxs-lookup"><span data-stu-id="935bd-162">In this section, you configure Data Lake Store access from HDInsight clusters using an Azure Active Directory service principal.</span></span> 

### <a name="specify-a-service-principal"></a><span data-ttu-id="935bd-163">指定服務主體</span><span class="sxs-lookup"><span data-stu-id="935bd-163">Specify a service principal</span></span>

<span data-ttu-id="935bd-164">從 Azure 入口網站中，您可以使用現有的服務主體或建立一個新的服務主體。</span><span class="sxs-lookup"><span data-stu-id="935bd-164">From the Azure portal, you can either use an existing service principal or create a new one.</span></span>

<span data-ttu-id="935bd-165">**從 Azure 入口網站中建立服務主體**</span><span class="sxs-lookup"><span data-stu-id="935bd-165">**To create a service principal from the Azure portal**</span></span>

1. <span data-ttu-id="935bd-166">從 [存放區] 刀鋒視窗中，按一下 [Data Lake Store 存取]。</span><span class="sxs-lookup"><span data-stu-id="935bd-166">Click **Data Lake Store access** from the Store blade.</span></span>
2. <span data-ttu-id="935bd-167">在 [Data Lake Store 存取] 刀鋒視窗中，按一下 [新建]。</span><span class="sxs-lookup"><span data-stu-id="935bd-167">On the **Data Lake Store access** blade, click **Create new**.</span></span>
3. <span data-ttu-id="935bd-168">按一下 [服務主體]，然後遵循指示建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="935bd-168">Click **Service Principal**, and then follow the instructions to create a service principal.</span></span>
4. <span data-ttu-id="935bd-169">如果您決定要在未來再次使用它，請下載憑證。</span><span class="sxs-lookup"><span data-stu-id="935bd-169">Download the certificate if you decide to use it again in the future.</span></span> <span data-ttu-id="935bd-170">如果您想要在建立其他 HDInsight 叢集時使用相同的服務主體，下載憑證非常實用。</span><span class="sxs-lookup"><span data-stu-id="935bd-170">Downloading the certificate is useful if you want to use the same service principal when you create additional HDInsight clusters.</span></span>

    <span data-ttu-id="935bd-171">![將服務主體新增至 HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "將服務主體新增至 HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="935bd-171">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Add service principal to HDInsight cluster")</span></span>

4. <span data-ttu-id="935bd-172">按一下 [存取] 來設定資料夾存取。</span><span class="sxs-lookup"><span data-stu-id="935bd-172">Click **Access** to configure the folder access.</span></span>  <span data-ttu-id="935bd-173">請參閱[設定檔案權限](#configure-file-permissions)。</span><span class="sxs-lookup"><span data-stu-id="935bd-173">See [Configure file permissions](#configure-file-permissions).</span></span>


<span data-ttu-id="935bd-174">**使用 Azure 入口網站中現有的服務主體**</span><span class="sxs-lookup"><span data-stu-id="935bd-174">**To use an existing service principal from the Azure portal**</span></span>

1. <span data-ttu-id="935bd-175">按一下 [Data Lake Store 存取]。</span><span class="sxs-lookup"><span data-stu-id="935bd-175">Click **Data Lake Store access**.</span></span>
1. <span data-ttu-id="935bd-176">在 [Data Lake Store 存取] 刀鋒視窗中，按一下 [Use existing] \(使用現有)。</span><span class="sxs-lookup"><span data-stu-id="935bd-176">On the **Data Lake Store access** blade, click **Use existing**.</span></span>
2. <span data-ttu-id="935bd-177">按一下 [服務主體]，然後選取一個服務主體。</span><span class="sxs-lookup"><span data-stu-id="935bd-177">Click **Service Principal**, and then select a service principal.</span></span> 
3. <span data-ttu-id="935bd-178">上傳與您所選取服務主體建立關聯的憑證 (.pfx 檔案)，然後輸入憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="935bd-178">Upload the certificate (.pfx file) that's associated with your selected service principal, and then enter the certificate password.</span></span>

    <span data-ttu-id="935bd-179">![將服務主體新增至 HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "將服務主體新增至 HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="935bd-179">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Add service principal to HDInsight cluster")</span></span>

4. <span data-ttu-id="935bd-180">按一下 [存取] 來設定資料夾存取。</span><span class="sxs-lookup"><span data-stu-id="935bd-180">Click **Access** to configure the folder access.</span></span>  <span data-ttu-id="935bd-181">請參閱[設定檔案權限](#configure-file-permissions)。</span><span class="sxs-lookup"><span data-stu-id="935bd-181">See [Configure file permissions](#configure-file-permissions).</span></span>


### <span data-ttu-id="935bd-182"><a name="configure-file-permissions"></a>設定檔案權限</span><span class="sxs-lookup"><span data-stu-id="935bd-182"><a name="configure-file-permissions"></a>Configure file permissions</span></span>

<span data-ttu-id="935bd-183">這些設定會視帳戶是作為預設儲存體帳戶還是其他儲存體帳戶而不同：</span><span class="sxs-lookup"><span data-stu-id="935bd-183">The configures are different depending on whether the account is used as the default storage or an additional storage account:</span></span>

- <span data-ttu-id="935bd-184">作為預設儲存體</span><span class="sxs-lookup"><span data-stu-id="935bd-184">Used as default storage</span></span>

    - <span data-ttu-id="935bd-185">Data Lake Store 帳戶根層級的權限</span><span class="sxs-lookup"><span data-stu-id="935bd-185">permission at the root level of the Data Lake Store account</span></span>
    - <span data-ttu-id="935bd-186">HDInsight 叢集儲存體根層級的權限。</span><span class="sxs-lookup"><span data-stu-id="935bd-186">permission at the root level of the HDInsight cluster storage.</span></span> <span data-ttu-id="935bd-187">例如，稍早在教學課程中使用的 __/clusters__ 資料夾。</span><span class="sxs-lookup"><span data-stu-id="935bd-187">For example, the __/clusters__ folder used earlier in the tutorial.</span></span>
- <span data-ttu-id="935bd-188">作為其他儲存體</span><span class="sxs-lookup"><span data-stu-id="935bd-188">Use as an additional storage</span></span>

    - <span data-ttu-id="935bd-189">您需要其檔案存取權之資料夾的權限。</span><span class="sxs-lookup"><span data-stu-id="935bd-189">Permission at the folders where you need file access.</span></span>

<span data-ttu-id="935bd-190">**指派 Data Lake Store 帳戶根層級的權限**</span><span class="sxs-lookup"><span data-stu-id="935bd-190">**To assign permission at the Data Lake Store account root level**</span></span>

1. <span data-ttu-id="935bd-191">在 [Data Lake Store 存取權] 刀鋒視窗中，按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="935bd-191">On the **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="935bd-192">隨即會開啟 [選取檔案權限] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="935bd-192">The **Select file permissions** blade is opened.</span></span> <span data-ttu-id="935bd-193">其中列出您訂用帳戶中的所有 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="935bd-193">It lists all the Data Lake Store accounts in your subscription.</span></span>
2. <span data-ttu-id="935bd-194">請將滑鼠游標暫留 (請勿按一下) 在 Data Lake Store 帳戶的名稱上，以顯示核取方塊，然後選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="935bd-194">Hover (do not click) the mouse over the name of the Data Lake Store account to make the check box visible, then select the check box.</span></span>

    <span data-ttu-id="935bd-195">![將服務主體新增至 HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "將服務主體新增至 HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="935bd-195">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Add service principal to HDInsight cluster")</span></span>

  <span data-ttu-id="935bd-196">根據預設，__READ__、__WRITE__ 和 __EXECUTE__ 會全部選取。</span><span class="sxs-lookup"><span data-stu-id="935bd-196">By default, __READ__, __WRITE__, AND __EXECUTE__ are all selected.</span></span>

3. <span data-ttu-id="935bd-197">按一下頁面底部的 [選取]。</span><span class="sxs-lookup"><span data-stu-id="935bd-197">Click **Select** on the bottom of the page.</span></span>
4. <span data-ttu-id="935bd-198">按一下 [執行] 來指派權限。</span><span class="sxs-lookup"><span data-stu-id="935bd-198">Click **Run** to assign permission.</span></span>
5. <span data-ttu-id="935bd-199">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="935bd-199">Click **Done**.</span></span>

<span data-ttu-id="935bd-200">**指派 HDInsight 叢集根層級的權限**</span><span class="sxs-lookup"><span data-stu-id="935bd-200">**To assign permission at the HDInsight cluster root level**</span></span>

1. <span data-ttu-id="935bd-201">在 [Data Lake Store 存取權] 刀鋒視窗中，按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="935bd-201">On the **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="935bd-202">隨即會開啟 [選取檔案權限] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="935bd-202">The **Select file permissions** blade is opened.</span></span> <span data-ttu-id="935bd-203">其中列出您訂用帳戶中的所有 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="935bd-203">It lists all the Data Lake Store accounts in your subscription.</span></span>
1. <span data-ttu-id="935bd-204">從 [選取檔案權限] 刀鋒視窗中，按一下要顯示其內容的 Data Lake Store 名稱。</span><span class="sxs-lookup"><span data-stu-id="935bd-204">From the **Select file permissions** blade, click the Data Lake Store name to show its content.</span></span>
2. <span data-ttu-id="935bd-205">選取 HDInsight 叢集儲存體根目錄左邊的核取方塊，即可選取該資料夾。</span><span class="sxs-lookup"><span data-stu-id="935bd-205">Select the HDInsight cluster storage root by selecting the checkbox on the left of the folder.</span></span> <span data-ttu-id="935bd-206">根據先前的螢幕擷取畫面，叢集儲存體根目錄為您在選取 Data Lake Store 作為預設儲存體時所指定的 __/clusters__ 資料夾。</span><span class="sxs-lookup"><span data-stu-id="935bd-206">According to the screenshot earlier, the cluster storage root is __/clusters__ folder that you specified while selecting the Data Lake Store as default storage.</span></span>
3. <span data-ttu-id="935bd-207">設定資料夾的權限。</span><span class="sxs-lookup"><span data-stu-id="935bd-207">Set the permissions on the folder.</span></span>  <span data-ttu-id="935bd-208">根據預設，讀取、寫入和執行會全部選取。</span><span class="sxs-lookup"><span data-stu-id="935bd-208">By default, read, write, and execute are all selected.</span></span>
4. <span data-ttu-id="935bd-209">按一下頁面底部的 [選取]。</span><span class="sxs-lookup"><span data-stu-id="935bd-209">Click **Select** on the bottom of the page.</span></span>
5. <span data-ttu-id="935bd-210">按一下 **[執行]**。</span><span class="sxs-lookup"><span data-stu-id="935bd-210">Click **Run**.</span></span>
6. <span data-ttu-id="935bd-211">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="935bd-211">Click **Done**.</span></span>

<span data-ttu-id="935bd-212">如果您使用 Data Lake Store 作為其他儲存體，則必須僅針對您想要從 HDInsight 叢集存取的資料夾指派權限。</span><span class="sxs-lookup"><span data-stu-id="935bd-212">If you are using Data Lake Store as additional storage, you must assign permission only for the folders that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="935bd-213">例如，在下方的螢幕擷取畫面中，您僅會將存取提供給 Data Lake Store 帳戶中的 **hdiaddonstorage** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="935bd-213">For example, in the screenshot below, you provide access only to **hdiaddonstorage** folder in a Data Lake Store account.</span></span>

<span data-ttu-id="935bd-214">![將服務主體權限指派給 HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "將服務主體權限指派給 HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="935bd-214">![Assign service principal permissions to the HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "Assign service principal permissions to the HDInsight cluster")</span></span>


## <a name="verify-cluster-set-up"></a><span data-ttu-id="935bd-215">確認叢集設定</span><span class="sxs-lookup"><span data-stu-id="935bd-215">Verify cluster set up</span></span>

<span data-ttu-id="935bd-216">叢集設定完成之後，在叢集刀鋒視窗上執行下列任一或這兩個步驟來驗證結果：</span><span class="sxs-lookup"><span data-stu-id="935bd-216">After the cluster setup is complete, on the cluster blade, verify your results by doing either or both of the following steps:</span></span>

* <span data-ttu-id="935bd-217">若要驗證叢集的相關儲存體是否為您指定的 Data Lake Store 帳戶，請按一下左窗格中的 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="935bd-217">To verify that the associated storage for the cluster is the Data Lake Store account that you specified, click **Storage accounts** in the left pane.</span></span>

    <span data-ttu-id="935bd-218">![將服務主體新增至 HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "將服務主體新增至 HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="935bd-218">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Add service principal to HDInsight cluster")</span></span>

* <span data-ttu-id="935bd-219">若要驗證服務主體是否正確地與 HDInsight 叢集相關聯，請按一下左窗格中的 [Data Lake Store 存取權]。</span><span class="sxs-lookup"><span data-stu-id="935bd-219">To verify that the service principal is correctly associated with the HDInsight cluster, click **Data Lake Store access** in the left pane.</span></span>

    <span data-ttu-id="935bd-220">![將服務主體新增至 HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "將服務主體新增至 HDInsight 叢集")</span><span class="sxs-lookup"><span data-stu-id="935bd-220">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Add service principal to HDInsight cluster")</span></span>


## <a name="examples"></a><span data-ttu-id="935bd-221">範例</span><span class="sxs-lookup"><span data-stu-id="935bd-221">Examples</span></span>

<span data-ttu-id="935bd-222">在您設定以 Data Lake Store 做為儲存體的叢集之後，請參考一些範例以了解如何使用 HDInsight 叢集來分析 Data Lake Store 中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="935bd-222">After you have set up the cluster with Data Lake Store as your storage, refer to these examples of how to use HDInsight cluster to analyze the data that's stored in Data Lake Store.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a><span data-ttu-id="935bd-223">針對 Data Lake Store (做為主要儲存體) 中的資料執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="935bd-223">Run a Hive query against data in a Data Lake Store (as primary storage)</span></span>

<span data-ttu-id="935bd-224">若要執行 Hive 查詢，請使用 Ambari 入口網站中的 Hive 檢視介面。</span><span class="sxs-lookup"><span data-stu-id="935bd-224">To run a Hive query, use the Hive views interface in the Ambari portal.</span></span> <span data-ttu-id="935bd-225">如需有關如何使用 Ambari Hive 檢視的指示，請參閱[在 HDInsight 中搭配 Hadoop 使用 Hive 檢視](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md)。</span><span class="sxs-lookup"><span data-stu-id="935bd-225">For instructions on how to use Ambari Hive views, see [Use the Hive View with Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

<span data-ttu-id="935bd-226">當您使用 Data Lake Store 中的資料時，有幾個字串需要變更。</span><span class="sxs-lookup"><span data-stu-id="935bd-226">When you work with data in a Data Lake Store, there are a few strings to change.</span></span>

<span data-ttu-id="935bd-227">如果您使用以 Data Lake Store 做為主要儲存體而建立的叢集，則資料路徑為︰adl://<data_lake_store_account_name>/azuredatalakestore.net/path/to/file。</span><span class="sxs-lookup"><span data-stu-id="935bd-227">If you use, for example, the cluster that you created with Data Lake Store as primary storage, the path to the data is: *adl://<data_lake_store_account_name>/azuredatalakestore.net/path/to/file*.</span></span> <span data-ttu-id="935bd-228">從 Data Lake Store 帳戶中儲存的範例資料建立資料表的 Hive 查詢，類似於下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="935bd-228">A Hive query to create a table from sample data that's stored in the Data Lake Store account looks like the following statement:</span></span>

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

<span data-ttu-id="935bd-229">說明：</span><span class="sxs-lookup"><span data-stu-id="935bd-229">Descriptions:</span></span>
* <span data-ttu-id="935bd-230">`adl://hdiadlstorage.azuredatalakestore.net/` 是 Data Lake Store 帳戶的根。</span><span class="sxs-lookup"><span data-stu-id="935bd-230">`adl://hdiadlstorage.azuredatalakestore.net/` is the root of the Data Lake Store account.</span></span>
* <span data-ttu-id="935bd-231">`/clusters/myhdiadlcluster` 是您在建立叢集時指定之叢集資料的根目錄。</span><span class="sxs-lookup"><span data-stu-id="935bd-231">`/clusters/myhdiadlcluster` is the root of the cluster data that you specified while creating the cluster.</span></span>
* <span data-ttu-id="935bd-232">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/` 是您在查詢中使用之範例檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="935bd-232">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/` is the location of the sample file that you used in the query.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a><span data-ttu-id="935bd-233">針對 Data Lake Store (做為額外儲存體) 中的資料執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="935bd-233">Run a Hive query against data in a Data Lake Store (as additional storage)</span></span>

<span data-ttu-id="935bd-234">如果您建立的叢集使用 Blob 儲存體做為預設儲存體，則範例資料不會包含在做為額外儲存體的 Azure Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="935bd-234">If the cluster that you created uses Blob storage as default storage, the sample data is not contained in the Azure Data Lake Store account that's used as additional storage.</span></span> <span data-ttu-id="935bd-235">在這種情況下，請先將資料從 Blob 儲存體傳送至 Data Lake Store，然後如上述範例所示執行查詢。</span><span class="sxs-lookup"><span data-stu-id="935bd-235">In such a case, first transfer the data from Blob storage to the Data Lake Store, and then run the queries as shown in the preceding example.</span></span>

<span data-ttu-id="935bd-236">如需如何將資料從 Blob 儲存體複製到 Data Lake Store 的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="935bd-236">For information on how to copy data from Blob storage to a Data Lake Store, see the following articles:</span></span>

* [<span data-ttu-id="935bd-237">使用 Distcp 在 Azure 儲存體 Blob 與 Data Lake Store 之間複製資料</span><span class="sxs-lookup"><span data-stu-id="935bd-237">Use Distcp to copy data between Azure Storage blobs and Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
* [<span data-ttu-id="935bd-238">使用 AdlCopy 將資料從 Azure 儲存體 Blob 複製到 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="935bd-238">Use AdlCopy to copy data from Azure Storage blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a><span data-ttu-id="935bd-239">使用 Data Lake Store 搭配 Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="935bd-239">Use Data Lake Store with a Spark cluster</span></span>
<span data-ttu-id="935bd-240">您可以使用 Spark 叢集對 Data Lake Store 中儲存的資料執行 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="935bd-240">You can use a Spark cluster to run Spark jobs on data that is stored in a Data Lake Store.</span></span> <span data-ttu-id="935bd-241">如需詳細資訊，請參閱[使用 HDInsight Spark 叢集來分析 Data Lake Store 中的資料](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="935bd-241">For more information, see [Use HDInsight Spark cluster to analyze data in Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).</span></span>


### <a name="use-data-lake-store-in-a-storm-topology"></a><span data-ttu-id="935bd-242">在 Storm 拓撲中使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="935bd-242">Use Data Lake Store in a Storm topology</span></span>
<span data-ttu-id="935bd-243">您可以使用 Data Lake Store 從 Storm 拓撲寫入資料。</span><span class="sxs-lookup"><span data-stu-id="935bd-243">You can use the Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="935bd-244">如需有關如何達到這種情況的指示，請參閱 [搭配使用 Azure Data Lake Store 與 HDInsight 上的 Apache Storm](../hdinsight/hdinsight-storm-write-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="935bd-244">For instructions on how to achieve this scenario, see [Use Azure Data Lake Store with Apache Storm with HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="935bd-245">另請參閱</span><span class="sxs-lookup"><span data-stu-id="935bd-245">See also</span></span>
* [<span data-ttu-id="935bd-246">PowerShell：建立 HDInsight 叢集以使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="935bd-246">PowerShell: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
