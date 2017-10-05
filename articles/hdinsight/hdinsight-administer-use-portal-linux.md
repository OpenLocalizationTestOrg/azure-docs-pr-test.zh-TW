---
title: "使用 Azure 入口網站管理 HDInsight 中的 Hadoop 叢集 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站來監視和管理 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c9cb631aef71f72457c3517d02566a56919f82bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a><span data-ttu-id="f689c-103">使用 Azure 入口網站管理 HDInsight 上的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-103">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="f689c-104">使用 [Azure 入口網站][azure-portal]，您可以管理 Azure HDInsight 中的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-104">Using the [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="f689c-105">使用索引標籤選取器，以取得使用其他工具管理 HDInsight 中 Hadoop 叢集的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f689c-105">Use the tab selector for information on managing Hadoop clusters in HDInsight using other tools.</span></span>

<span data-ttu-id="f689c-106">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="f689c-106">**Prerequisites**</span></span>

<span data-ttu-id="f689c-107">開始閱讀本文之前，您必須有下列各項：</span><span class="sxs-lookup"><span data-stu-id="f689c-107">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="f689c-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f689c-108">**An Azure subscription**.</span></span> <span data-ttu-id="f689c-109">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="f689c-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="open-the-portal"></a><span data-ttu-id="f689c-110">開啟入口網站</span><span class="sxs-lookup"><span data-stu-id="f689c-110">Open the portal</span></span>
1. <span data-ttu-id="f689c-111">登入 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f689c-111">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f689c-112">開啟入口網站之後，您可以：</span><span class="sxs-lookup"><span data-stu-id="f689c-112">After you open the portal, you can:</span></span>

   * <span data-ttu-id="f689c-113">按一下左功能表中的 [新增]  以建立新的叢集：</span><span class="sxs-lookup"><span data-stu-id="f689c-113">Click **New** from the left menu to create a new cluster:</span></span>

       ![新的 HDInsight 叢集按鈕](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * <span data-ttu-id="f689c-115">按一下左側功能表中的 [HDInsight 叢集]  以列出現有的叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-115">Click **HDInsight Clusters** from the left menu to list the existing clusters</span></span>

       ![Azure 入口網站 HDInsight 叢集按鈕](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       <span data-ttu-id="f689c-117">如果您沒有看見 HDInsight 叢集，請按一下位於清單底部的 [更多服務]，然後按一下位於 [智慧 + 分析] 區段底下的 [HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="f689c-117">If you don't see HDInsight cluster, click **More services** on the bottom of the list, and then click **HDInsight clusters** under the **Intelligence + Analytics** section.</span></span>


## <a name="create-clusters"></a><span data-ttu-id="f689c-118">建立叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-118">Create clusters</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="f689c-119">HDInsight 可以與很多 Hadoop 元件搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f689c-119">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="f689c-120">如需已驗證和所支援元件的清單，請參閱 [Azure HDInsight 提供 Hadoop 的什麼版本？](hdinsight-component-versioning.md)(英文)。</span><span class="sxs-lookup"><span data-stu-id="f689c-120">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="f689c-121">如需一般叢集建立的資訊，請參閱 [在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-121">For the general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="f689c-122">存取控制需求</span><span class="sxs-lookup"><span data-stu-id="f689c-122">Access control requirements</span></span>

<span data-ttu-id="f689c-123">當您建立 HDInsight 叢集時，必須指定 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f689c-123">You must specify an Azure subscription when you create an HDInsight cluster.</span></span> <span data-ttu-id="f689c-124">這個叢集可在新的 Azure 資源群組中建立，或是在現有的資源群組中建立。</span><span class="sxs-lookup"><span data-stu-id="f689c-124">This cluster can be created in either a new Azure Resource group or an existing Resource group.</span></span> <span data-ttu-id="f689c-125">您可以使用下列步驟，確認您具有建立 HDInsight 叢集的權限：</span><span class="sxs-lookup"><span data-stu-id="f689c-125">You can use the following steps to verify your permissions for creating HDInsight clusters:</span></span>

- <span data-ttu-id="f689c-126">使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f689c-126">To use an existing resource group.</span></span>

    1. <span data-ttu-id="f689c-127">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f689c-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="f689c-128">按一下左側功能表的 [資源群組] 以列出資源群組。</span><span class="sxs-lookup"><span data-stu-id="f689c-128">Click **Resource groups** from the left menu to list the resource groups.</span></span>
    3. <span data-ttu-id="f689c-129">按一下您要用來建立 HDInsight 叢集的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f689c-129">Click the resource group you want to use for creating your HDInsight cluster.</span></span>
    4. <span data-ttu-id="f689c-130">按一下 [存取控制 (IAM)]，然後確認您 (或是您所屬的群組) 至少具有資源群組的「參與者」存取權限。</span><span class="sxs-lookup"><span data-stu-id="f689c-130">Click **Access control (IAM)**, and verify that you (or a group that you belong to) have at least the Contributor access to the resource group.</span></span>

- <span data-ttu-id="f689c-131">建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="f689c-131">To create a new resource group</span></span>

    1. <span data-ttu-id="f689c-132">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f689c-132">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="f689c-133">按一下左側功能表的 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f689c-133">Click **Subscription** from the left menu.</span></span> <span data-ttu-id="f689c-134">它有黃色的鑰匙圖示。</span><span class="sxs-lookup"><span data-stu-id="f689c-134">It has a yellow key icon.</span></span> <span data-ttu-id="f689c-135">您應該會看到訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="f689c-135">You shall see a list of subscriptions.</span></span>
    3. <span data-ttu-id="f689c-136">按一下您要用來建立叢集的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f689c-136">Click the subscription that you use to create clusters.</span></span> 
    4. <span data-ttu-id="f689c-137">按一下 [我的權限]。</span><span class="sxs-lookup"><span data-stu-id="f689c-137">Click **My permissions**.</span></span>  <span data-ttu-id="f689c-138">它會顯示您在訂用帳戶上的[角色](../active-directory/role-based-access-control-what-is.md#built-in-roles)。</span><span class="sxs-lookup"><span data-stu-id="f689c-138">It shows your [role](../active-directory/role-based-access-control-what-is.md#built-in-roles) on the subscription.</span></span> <span data-ttu-id="f689c-139">您至少需要「參與者」存取權限才能建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-139">You need at least Contributor access to create HDInsight cluster.</span></span>

<span data-ttu-id="f689c-140">如果您收到 NoRegisteredProviderFound 錯誤或 MissingSubscriptionRegistration 錯誤，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](../azure-resource-manager/resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-140">If you receive the NoRegisteredProviderFound error or the MissingSubscriptionRegistration error, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="f689c-141">列出和顯示叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-141">List and show clusters</span></span>
1. <span data-ttu-id="f689c-142">登入 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f689c-142">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f689c-143">按一下左側功能表中的 [HDInsight 叢集]  以列出現有的叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-143">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="f689c-144">按一下叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f689c-144">Click the cluster name.</span></span> <span data-ttu-id="f689c-145">如果叢集清單很長，您可以使用頁面頂端的篩選器。</span><span class="sxs-lookup"><span data-stu-id="f689c-145">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="f689c-146">按一下清單中的叢集以顯示概觀頁面：</span><span class="sxs-lookup"><span data-stu-id="f689c-146">Click a cluster from the list to see the overview page:</span></span>

    ![Azure portal HDInsight cluster essentials](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * <span data-ttu-id="f689c-148">**儀表板**：開啟叢集儀表板，這是適用於以 Linux 為基礎之叢集的 Ambari Web。</span><span class="sxs-lookup"><span data-stu-id="f689c-148">**Dashboard**: Opens the cluster dashboard, which is Ambari Web for Linux-based clusters.</span></span>
    * <span data-ttu-id="f689c-149">**安全殼層**︰顯示使用安全殼層 (SSH) 連線連接到叢集的指示。</span><span class="sxs-lookup"><span data-stu-id="f689c-149">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span>
    * <span data-ttu-id="f689c-150">**調整叢集**：可讓您變更此叢集的背景工作節點數目。</span><span class="sxs-lookup"><span data-stu-id="f689c-150">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span></span>
    * <span data-ttu-id="f689c-151">**刪除**：刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-151">**Delete**: Deletes the cluster.</span></span>
    * <span data-ttu-id="f689c-152">**活動記錄檔**︰顯示和查詢活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f689c-152">**Activity logs**: Show and query activity logs.</span></span>
    * <span data-ttu-id="f689c-153">**存取控制 (IAM)**︰使用角色指派。</span><span class="sxs-lookup"><span data-stu-id="f689c-153">**Access control (IAM)**: Use role assignments.</span></span>  <span data-ttu-id="f689c-154">請參閱[使用角色指派來管理 Azure 訂用帳戶資源的存取權](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-154">See [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
    * <span data-ttu-id="f689c-155">**標記**：可讓您設定索引鍵/值組，以定義自訂的雲端服務分類法。</span><span class="sxs-lookup"><span data-stu-id="f689c-155">**Tags**: Allows you to set key/value pairs to define a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="f689c-156">例如，您可建立名為 **project**的索引鍵，然後使用與特定專案相關聯之所有服務的通用值。</span><span class="sxs-lookup"><span data-stu-id="f689c-156">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
    * <span data-ttu-id="f689c-157">**診斷並解決問題**︰顯示疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="f689c-157">**Diagnose and solve problems**: Display troubleshooting information.</span></span>
    * <span data-ttu-id="f689c-158">**鎖定**︰新增鎖定以防止叢集遭到修改或刪除。</span><span class="sxs-lookup"><span data-stu-id="f689c-158">**Locks**: Add lock to prevent the cluster being modified or deleted.</span></span>
    * <span data-ttu-id="f689c-159">**自動化指令碼**︰顯示和匯出叢集的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="f689c-159">**Automation script**: Display and export the Azure Resource Manager template for the cluster.</span></span> <span data-ttu-id="f689c-160">目前，您只能匯出相依的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f689c-160">Currently, you can only export the dependent Azure storage account.</span></span> <span data-ttu-id="f689c-161">請參閱[使用 Azure Resource Manager 範本在 HDInsight 中建立 Linux 型 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-161">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>
    * <span data-ttu-id="f689c-162">**快速啟動**：顯示可協助您開始使用 HDInsight 的資訊。</span><span class="sxs-lookup"><span data-stu-id="f689c-162">**Quick Start**:  Displays information that helps you get started using HDInsight.</span></span>
    * <span data-ttu-id="f689c-163">**適用於 HDInsight 的工具**：HDInsight 相關工具的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="f689c-163">**Tools for HDInsight**: Help information for HDInsight related tools.</span></span>
    * <span data-ttu-id="f689c-164">**叢集登入**︰顯示叢集登入資訊。</span><span class="sxs-lookup"><span data-stu-id="f689c-164">**Cluster Login**: Display the cluster login information.</span></span>
    * <span data-ttu-id="f689c-165">**訂用帳戶核心使用量**︰顯示訂用帳戶的已使用和可用核心。</span><span class="sxs-lookup"><span data-stu-id="f689c-165">**Subscription Core Usage**: Display the used and available cores for your subscription.</span></span>
    * <span data-ttu-id="f689c-166">**調整叢集**：增加和減少叢集背景工作角色節點的數目。</span><span class="sxs-lookup"><span data-stu-id="f689c-166">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span></span> <span data-ttu-id="f689c-167">請參閱[調整叢集](hdinsight-administer-use-management-portal.md#scale-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f689c-167">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span></span>
    * <span data-ttu-id="f689c-168">**安全殼層**︰顯示使用安全殼層 (SSH) 連線連接到叢集的指示。</span><span class="sxs-lookup"><span data-stu-id="f689c-168">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span> <span data-ttu-id="f689c-169">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-169">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
    * <span data-ttu-id="f689c-170">**HDInsight 合作夥伴**︰新增/移除目前的 HDInsight 合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="f689c-170">**HDInsight Partner**: Add/remove the current HDInsight Partner.</span></span>
    * <span data-ttu-id="f689c-171">**外部中繼存放區**：檢視 Hive 和 Oozie 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="f689c-171">**External Metastores**: View the Hive and Oozie metastores.</span></span> <span data-ttu-id="f689c-172">中繼存放區只可以在叢集建立程序期間進行設定。</span><span class="sxs-lookup"><span data-stu-id="f689c-172">The metastores can only be configured during the cluster creation process.</span></span> <span data-ttu-id="f689c-173">請參閱[使用 Hive/Oozie 中繼存放區](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore)。</span><span class="sxs-lookup"><span data-stu-id="f689c-173">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span></span>
    * <span data-ttu-id="f689c-174">**指令碼動作**︰在叢集上執行 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f689c-174">**Script Actions**: Run Bash scripts on the cluster.</span></span> <span data-ttu-id="f689c-175">請參閱 [使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-175">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    * <span data-ttu-id="f689c-176">**應用程式**：新增/移除 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f689c-176">**Applications**: Add/remove HDInsight applications.</span></span>  <span data-ttu-id="f689c-177">請參閱[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-177">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
    * <span data-ttu-id="f689c-178">**屬性**：檢視叢集屬性。</span><span class="sxs-lookup"><span data-stu-id="f689c-178">**Properties**: View the cluster properties.</span></span>
    * <span data-ttu-id="f689c-179">**儲存體帳戶**︰檢視儲存體帳戶和金鑰。</span><span class="sxs-lookup"><span data-stu-id="f689c-179">**Storage accounts**: View the storage accounts and the keys.</span></span> <span data-ttu-id="f689c-180">儲存體帳戶是在進行叢集建立程序時設定。</span><span class="sxs-lookup"><span data-stu-id="f689c-180">The storage accounts are configured during the cluster creation process.</span></span>
    * <span data-ttu-id="f689c-181">**叢集 AAD 身分識別**：</span><span class="sxs-lookup"><span data-stu-id="f689c-181">**Cluster AAD Identity**:</span></span>
    * <span data-ttu-id="f689c-182">**新的支援要求**︰可讓您透過 Microsoft 支援服務建立支援票證。</span><span class="sxs-lookup"><span data-stu-id="f689c-182">**New support request**: Allows you to create a support ticket with Microsoft support.</span></span>
    
6. <span data-ttu-id="f689c-183">按一下 [屬性] ：</span><span class="sxs-lookup"><span data-stu-id="f689c-183">Click **Properties**:</span></span>

    <span data-ttu-id="f689c-184">屬性如下︰</span><span class="sxs-lookup"><span data-stu-id="f689c-184">The properties are:</span></span>

   * <span data-ttu-id="f689c-185">**主機名稱**：叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f689c-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="f689c-186">**叢集 URL**。</span><span class="sxs-lookup"><span data-stu-id="f689c-186">**Cluster URL**.</span></span> <span data-ttu-id="f689c-187">Ambari Web 介面的 URL。</span><span class="sxs-lookup"><span data-stu-id="f689c-187">The URL for the Ambari web interface.</span></span>
   * <span data-ttu-id="f689c-188">**狀態**：包括Aborted、Accepted、ClusterStorageProvisioned、AzureVMConfiguration、HDInsightConfiguration、Operational、Running、Error、Deleting、Deleted、Timedout、DeleteQueued、DeleteTimedout、DeleteError、PatchQueued、CertRolloverQueued、ResizeQueued、ClusterCustomization</span><span class="sxs-lookup"><span data-stu-id="f689c-188">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="f689c-189">**區域**：Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="f689c-189">**Region**: Azure location.</span></span> <span data-ttu-id="f689c-190">如需支援的 Azure 位置清單，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)上的 [區域] 下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="f689c-190">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="f689c-191">**建立日期**。</span><span class="sxs-lookup"><span data-stu-id="f689c-191">**Date created**.</span></span>
   * <span data-ttu-id="f689c-192">**作業系統**：**Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="f689c-192">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="f689c-193">**類型**：Hadoop、HBase、Storm、Spark。</span><span class="sxs-lookup"><span data-stu-id="f689c-193">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="f689c-194">**版本**。</span><span class="sxs-lookup"><span data-stu-id="f689c-194">**Version**.</span></span> <span data-ttu-id="f689c-195">請參閱 [HDInsight 版本](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="f689c-195">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="f689c-196">**訂用帳戶**︰訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f689c-196">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="f689c-197">**預設資料來源**︰預設叢集檔案系統。</span><span class="sxs-lookup"><span data-stu-id="f689c-197">**Default data source**: The default cluster file system.</span></span>
   * <span data-ttu-id="f689c-198">**背景工作節點**。</span><span class="sxs-lookup"><span data-stu-id="f689c-198">**Worker nodes size**.</span></span>
   * <span data-ttu-id="f689c-199">**前端節點大小**。</span><span class="sxs-lookup"><span data-stu-id="f689c-199">**Head node size**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="f689c-200">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-200">Delete clusters</span></span>
<span data-ttu-id="f689c-201">刪除叢集時，並不會刪除預設的儲存體帳戶或任何連結的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f689c-201">Deleting a cluster does not delete the default storage account or any linked storage accounts.</span></span> <span data-ttu-id="f689c-202">您可以使用相同的儲存體帳戶和相同的中繼存放區重新建立叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-202">You can re-create the cluster by using the same storage accounts and the same metastores.</span></span> <span data-ttu-id="f689c-203">建議您在重新建立叢集時使用新的預設 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="f689c-203">It is recommended to use a new default Blob container when you re-create the cluster.</span></span>

1. <span data-ttu-id="f689c-204">登入[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f689c-204">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f689c-205">按一下左功能表中的 [HDInsight 叢集]  。</span><span class="sxs-lookup"><span data-stu-id="f689c-205">Click **HDInsight Clusters** from the left menu.</span></span> <span data-ttu-id="f689c-206">如果您沒有看到 [HDInsight 叢集]，可先按一下 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="f689c-206">If you don't see **HDInsight Clusters**, click **More services** first.</span></span>
3. <span data-ttu-id="f689c-207">按一下您想要刪除的叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-207">Click the cluster that you want to delete.</span></span>
4. <span data-ttu-id="f689c-208">按一下頂端功能表中的 [刪除]  ，然後依照指示執行。</span><span class="sxs-lookup"><span data-stu-id="f689c-208">Click **Delete** from the top menu, and then follow the instructions.</span></span>

<span data-ttu-id="f689c-209">另請參閱 [暫停/關閉叢集](#pauseshut-down-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f689c-209">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="f689c-210">新增其他儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f689c-210">Add additional storage accounts</span></span>

<span data-ttu-id="f689c-211">建立叢集之後，您可以新增其他 Azure 儲存體帳戶和 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f689c-211">You can add additional Azure Storage accounts and Azure Data Lake Store accounts after a cluster is created.</span></span> <span data-ttu-id="f689c-212">如需詳細資訊，請參閱[將其他儲存體帳戶新增至 HDInsight](./hdinsight-hadoop-add-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-212">For more information, see [Add additional storage accounts to HDInsight](./hdinsight-hadoop-add-storage.md).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="f689c-213">調整叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-213">Scale clusters</span></span>
<span data-ttu-id="f689c-214">叢集調整功能可讓您變更在 Azure HDInsight 中執行的叢集所用的背景工作節點數目，而不需要重新建立叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-214">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f689c-215">只支援使用 HDInsight 3.1.3 版或更高版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-215">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="f689c-216">如果不確定您的叢集版本，您可以檢查 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="f689c-216">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="f689c-217">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f689c-217">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="f689c-218">變更 HDInsight 支援的每一種叢集所用的資料節點數目會有何影響：</span><span class="sxs-lookup"><span data-stu-id="f689c-218">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="f689c-219">Hadoop</span><span class="sxs-lookup"><span data-stu-id="f689c-219">Hadoop</span></span>

    <span data-ttu-id="f689c-220">您可以順暢地增加正在執行的 Hadoop 叢集中背景工作節點數目，而不會影響任何擱置或執行中的工作。</span><span class="sxs-lookup"><span data-stu-id="f689c-220">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="f689c-221">您也可以在作業進行當中提交新工作。</span><span class="sxs-lookup"><span data-stu-id="f689c-221">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="f689c-222">系統會順暢處理失敗的調整作業，讓叢集永保正常運作狀態。</span><span class="sxs-lookup"><span data-stu-id="f689c-222">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="f689c-223">減少資料節點數目以縮減 Hadoop 叢集時，系統會重新啟動叢集中的部分服務。</span><span class="sxs-lookup"><span data-stu-id="f689c-223">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="f689c-224">此行為會導致所有執行中和擱置的工作在調整作業完成時失敗。</span><span class="sxs-lookup"><span data-stu-id="f689c-224">This behavior causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="f689c-225">但您可以在作業完成後重新提交這些工作。</span><span class="sxs-lookup"><span data-stu-id="f689c-225">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="f689c-226">HBase</span><span class="sxs-lookup"><span data-stu-id="f689c-226">HBase</span></span>

    <span data-ttu-id="f689c-227">您可以順暢地在 HBase 叢集運作時對其新增或移除資料節點。</span><span class="sxs-lookup"><span data-stu-id="f689c-227">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="f689c-228">區域伺服器會在完成調整作業的數分鐘之內自動取得平衡。</span><span class="sxs-lookup"><span data-stu-id="f689c-228">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="f689c-229">但是，您也可以手動平衡區域伺服器，方法是登入叢集的前端節點，然後從命令提示字元視窗執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f689c-229">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="f689c-230">如需使用 HBase 殼層的詳細資訊，請參閱 []</span><span class="sxs-lookup"><span data-stu-id="f689c-230">For more information on using the HBase shell, see []</span></span>
* <span data-ttu-id="f689c-231">Storm</span><span class="sxs-lookup"><span data-stu-id="f689c-231">Storm</span></span>

    <span data-ttu-id="f689c-232">您可以順暢地在 Storm 叢集運作時對其新增或移除資料節點。</span><span class="sxs-lookup"><span data-stu-id="f689c-232">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="f689c-233">但在調整作業順利完成後，您需要重新平衡拓撲。</span><span class="sxs-lookup"><span data-stu-id="f689c-233">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="f689c-234">您可以使用兩種方式來完成重新平衡作業：</span><span class="sxs-lookup"><span data-stu-id="f689c-234">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="f689c-235">Storm Web UI</span><span class="sxs-lookup"><span data-stu-id="f689c-235">Storm web UI</span></span>
  * <span data-ttu-id="f689c-236">命令列介面 (CLI) 工具</span><span class="sxs-lookup"><span data-stu-id="f689c-236">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="f689c-237">如需詳細資訊，請參閱 [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 。</span><span class="sxs-lookup"><span data-stu-id="f689c-237">Refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="f689c-238">HDInsight 叢集上有提供 Storm Web UI：</span><span class="sxs-lookup"><span data-stu-id="f689c-238">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight Storm 調整重新平衡](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="f689c-240">以下是如何使用 CLI 命令重新平衡 Storm 拓撲的範例：</span><span class="sxs-lookup"><span data-stu-id="f689c-240">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="f689c-241">**調整叢集**</span><span class="sxs-lookup"><span data-stu-id="f689c-241">**To scale clusters**</span></span>

1. <span data-ttu-id="f689c-242">登入[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f689c-242">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f689c-243">按一下左功能表中的 [HDInsight 叢集]  。</span><span class="sxs-lookup"><span data-stu-id="f689c-243">Click **HDInsight Clusters** from the left menu.</span></span>
3. <span data-ttu-id="f689c-244">按一下您想要調整的叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-244">Click the cluster you want to scale.</span></span>
3. <span data-ttu-id="f689c-245">按一下 [調整叢集]。</span><span class="sxs-lookup"><span data-stu-id="f689c-245">Click **Scale Cluster**.</span></span>
4. <span data-ttu-id="f689c-246">輸入 **背景工作節點的數目**。</span><span class="sxs-lookup"><span data-stu-id="f689c-246">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="f689c-247">叢集節點的數目限制會因 Azure 訂用帳戶而有所不同。</span><span class="sxs-lookup"><span data-stu-id="f689c-247">The limit on the number of cluster nodes varies among Azure subscriptions.</span></span> <span data-ttu-id="f689c-248">請連絡帳務支援提高限制。</span><span class="sxs-lookup"><span data-stu-id="f689c-248">You can contact billing support to increase the limit.</span></span>  <span data-ttu-id="f689c-249">成本資訊會反映您對節點數目所做的變更。</span><span class="sxs-lookup"><span data-stu-id="f689c-249">The cost information reflects the changes you have made to the number of nodes.</span></span>

    ![HDInsight hadoop hbase storm spark scale](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="f689c-251">暫停/關閉叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-251">Pause/shut down clusters</span></span>

<span data-ttu-id="f689c-252">大部分 Hadoop 工作是只會偶爾執行的批次工作。</span><span class="sxs-lookup"><span data-stu-id="f689c-252">Most of Hadoop jobs are batch jobs that are only run occasionally.</span></span> <span data-ttu-id="f689c-253">對於大部分的 Hadoop 叢集而言，叢集長時間並未用於處理。</span><span class="sxs-lookup"><span data-stu-id="f689c-253">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span></span> <span data-ttu-id="f689c-254">利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。</span><span class="sxs-lookup"><span data-stu-id="f689c-254">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="f689c-255">您也需支付 HDInsight 叢集的費用 (即使未使用)。</span><span class="sxs-lookup"><span data-stu-id="f689c-255">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="f689c-256">由於叢集費用是儲存體費用的許多倍，所以刪除未使用的叢集符合經濟效益。</span><span class="sxs-lookup"><span data-stu-id="f689c-256">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="f689c-257">有許多方法可以設計程序：</span><span class="sxs-lookup"><span data-stu-id="f689c-257">There are many ways you can program the process:</span></span>

* <span data-ttu-id="f689c-258">使用 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="f689c-258">User Azure Data Factory.</span></span> <span data-ttu-id="f689c-259">如需建立隨選 HDInsight 連結服務，請參閱 [使用 Azure Data Factory 在 HDInsight 中建立 Linux 型隨選 Handooop 叢集](hdinsight-hadoop-create-linux-clusters-adf.md) 。</span><span class="sxs-lookup"><span data-stu-id="f689c-259">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span></span>
* <span data-ttu-id="f689c-260">使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f689c-260">Use Azure PowerShell.</span></span>  <span data-ttu-id="f689c-261">請參閱 [分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-261">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="f689c-262">使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f689c-262">Use Azure CLI.</span></span> <span data-ttu-id="f689c-263">請參閱 [使用 Azure CLI 管理 HDInsight 叢集](hdinsight-administer-use-command-line.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-263">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="f689c-264">使用 HDInsight .NET SDK。</span><span class="sxs-lookup"><span data-stu-id="f689c-264">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="f689c-265">請參閱 [提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-265">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="f689c-266">如需定價資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="f689c-266">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="f689c-267">若要從入口網站刪除叢集，請參閱 [刪除叢集](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="f689c-267">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span></span>


## <a name="upgrade-clusters"></a><span data-ttu-id="f689c-268">升級叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-268">Upgrade clusters</span></span>

<span data-ttu-id="f689c-269">請參閱[將 HDInsight 叢集升級為更新的版本](./hdinsight-upgrade-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-269">See [Upgrade HDInsight cluster to a newer version](./hdinsight-upgrade-cluster.md).</span></span>

## <a name="change-passwords"></a><span data-ttu-id="f689c-270">變更密碼</span><span class="sxs-lookup"><span data-stu-id="f689c-270">Change passwords</span></span>
<span data-ttu-id="f689c-271">HDInsight 叢集可以有兩個使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f689c-271">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="f689c-272">HDInsight 叢集使用者帳戶 (A.K.A.</span><span class="sxs-lookup"><span data-stu-id="f689c-272">The HDInsight cluster user account (A.K.A.</span></span> <span data-ttu-id="f689c-273">HTTP 使用者帳戶) 以及 SSH 使用者帳戶都會在建立程序期間建立。</span><span class="sxs-lookup"><span data-stu-id="f689c-273">HTTP user account) and the SSH user account are created during the creation process.</span></span> <span data-ttu-id="f689c-274">您可以使用 Ambari Web UI 來變更叢集使用者帳戶的使用者名稱、密碼，以及用於變更 SSH 使用者帳戶的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="f689c-274">You can use the Ambari web UI to change the cluster user account username and password, and script actions to change the SSH user account</span></span>

### <a name="change-the-cluster-user-password"></a><span data-ttu-id="f689c-275">變更叢集使用者密碼</span><span class="sxs-lookup"><span data-stu-id="f689c-275">Change the cluster user password</span></span>
<span data-ttu-id="f689c-276">您可以使用 Ambari Web UI 來變更叢集使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="f689c-276">You can use the Ambari Web UI to change the Cluster user password.</span></span> <span data-ttu-id="f689c-277">若要登入 Ambari，您必須使用現有的叢集使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f689c-277">To log in to Ambari, you must use the existing cluster username and password.</span></span>

> [!NOTE]
> <span data-ttu-id="f689c-278">變更叢集使用者 (管理員) 密碼可能會造成針對此叢集執行的指令碼動作失敗。</span><span class="sxs-lookup"><span data-stu-id="f689c-278">Changing the cluster user (admin) password may cause script actions ran against this cluster to fail.</span></span> <span data-ttu-id="f689c-279">如果您有任何以背景工作節點為目標的持續性指令碼動作，當您透過調整大小作業新增節點到叢集，這些指令碼可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="f689c-279">If you have any persisted script actions that target worker nodes, these scripts may fail when you add nodes to the cluster through resize operations.</span></span> <span data-ttu-id="f689c-280">如需指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f689c-280">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="f689c-281">使用 HDInsight 叢集使用者認證登入 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="f689c-281">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="f689c-282">預設的使用者名稱為 **admin**。URL 是 **https://&lt;HDInsight 叢集名稱>azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="f689c-282">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="f689c-283">按一下頂端功能表中的 [管理]  ，然後按一下 [管理 Ambari]。</span><span class="sxs-lookup"><span data-stu-id="f689c-283">Click **Admin** from the top menu, and then click "Manage Ambari".</span></span>
3. <span data-ttu-id="f689c-284">按一下左側功能表中的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="f689c-284">From the left menu, click **Users**.</span></span>
4. <span data-ttu-id="f689c-285">按一下 Admin 。</span><span class="sxs-lookup"><span data-stu-id="f689c-285">Click **Admin**.</span></span>
5. <span data-ttu-id="f689c-286">按一下 [變更密碼] 。</span><span class="sxs-lookup"><span data-stu-id="f689c-286">Click **Change Password**.</span></span>

<span data-ttu-id="f689c-287">Ambari 會變更叢集中所有節點上的密碼。</span><span class="sxs-lookup"><span data-stu-id="f689c-287">Ambari then changes the password on all nodes in the cluster.</span></span>

### <a name="change-the-ssh-user-password"></a><span data-ttu-id="f689c-288">變更 SSH 使用者密碼</span><span class="sxs-lookup"><span data-stu-id="f689c-288">Change the SSH user password</span></span>
1. <span data-ttu-id="f689c-289">使用文字編輯器，將下列文字儲存為檔案並命名為 **changepassword.sh**。</span><span class="sxs-lookup"><span data-stu-id="f689c-289">Using a text editor, save the following text as a file named **changepassword.sh**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f689c-290">您必須使用行尾結束符號為 LF 的編輯器。</span><span class="sxs-lookup"><span data-stu-id="f689c-290">You must use an editor that uses LF as the line ending.</span></span> <span data-ttu-id="f689c-291">如果編輯器使用 CRLF，指令碼會無法運作。</span><span class="sxs-lookup"><span data-stu-id="f689c-291">If the editor uses CRLF, then the script does not work.</span></span>
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. <span data-ttu-id="f689c-292">將檔案上傳至可以使用 HTTP 或 HTTPS 位址從 HDInsight 存取的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="f689c-292">Upload the file to a storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span></span> <span data-ttu-id="f689c-293">例如，OneDrive 或 Azure Blob 儲存體這類的公用檔案存放區。</span><span class="sxs-lookup"><span data-stu-id="f689c-293">For example, a public file store such as OneDrive or Azure Blob storage.</span></span> <span data-ttu-id="f689c-294">將 URI (HTTP 或 HTTPS 位址) 儲存至檔案，在下一個步驟需用到此 URI。</span><span class="sxs-lookup"><span data-stu-id="f689c-294">Save the URI (HTTP or HTTPS address) to the file, as this URI is needed in the next step.</span></span>
3. <span data-ttu-id="f689c-295">從 Azure 入口網站，按一下 [HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="f689c-295">From the Azure portal, click **HDInsight Clusters**.</span></span>
4. <span data-ttu-id="f689c-296">按一下您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-296">Click your HDInsight cluster.</span></span>
4. <span data-ttu-id="f689c-297">按一下 [指令碼動作]。</span><span class="sxs-lookup"><span data-stu-id="f689c-297">Click **Script Actions**.</span></span>
4. <span data-ttu-id="f689c-298">從 [指令碼動作] 刀鋒視窗中，選取 [提交新的]。</span><span class="sxs-lookup"><span data-stu-id="f689c-298">From the **Script Actions** blade, select **Submit New**.</span></span> <span data-ttu-id="f689c-299">[提交指令碼動作] 刀鋒視窗出現後，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="f689c-299">When the **Submit script action** blade appears, enter the following information:</span></span>

   | <span data-ttu-id="f689c-300">欄位</span><span class="sxs-lookup"><span data-stu-id="f689c-300">Field</span></span> | <span data-ttu-id="f689c-301">值</span><span class="sxs-lookup"><span data-stu-id="f689c-301">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="f689c-302">Name</span><span class="sxs-lookup"><span data-stu-id="f689c-302">Name</span></span> |<span data-ttu-id="f689c-303">變更 SSH 密碼</span><span class="sxs-lookup"><span data-stu-id="f689c-303">Change ssh password</span></span> |
   | <span data-ttu-id="f689c-304">Bash 指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="f689c-304">Bash script URI</span></span> |<span data-ttu-id="f689c-305">changepassword.sh 檔案的 URI</span><span class="sxs-lookup"><span data-stu-id="f689c-305">The URI to the changepassword.sh file</span></span> |
   | <span data-ttu-id="f689c-306">節點 (前端、背景工作、Nimbus、監督員、Zookeeper 等)</span><span class="sxs-lookup"><span data-stu-id="f689c-306">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span></span> |<span data-ttu-id="f689c-307">✓ 針對列出的所有節點類型</span><span class="sxs-lookup"><span data-stu-id="f689c-307">✓ for all node types listed</span></span> |
   | <span data-ttu-id="f689c-308">參數</span><span class="sxs-lookup"><span data-stu-id="f689c-308">Parameters</span></span> |<span data-ttu-id="f689c-309">輸入 SSH 使用者名稱，然後輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="f689c-309">Enter the SSH user name and then the new password.</span></span> <span data-ttu-id="f689c-310">使用者名稱和密碼之間應該有一個空格。</span><span class="sxs-lookup"><span data-stu-id="f689c-310">There should be one space between the user name and the password.</span></span> |
   | <span data-ttu-id="f689c-311">保存這個指令碼動作...</span><span class="sxs-lookup"><span data-stu-id="f689c-311">Persist this script action ...</span></span> |<span data-ttu-id="f689c-312">不選取此欄位。</span><span class="sxs-lookup"><span data-stu-id="f689c-312">Leave this field unchecked.</span></span> |
5. <span data-ttu-id="f689c-313">按一下 [建立] 套用指令碼。</span><span class="sxs-lookup"><span data-stu-id="f689c-313">Select **Create** to apply the script.</span></span> <span data-ttu-id="f689c-314">指令碼完成後，您可以使用 SSH 與新密碼連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-314">Once the script finishes, you are able to connect to the cluster using SSH with the new password.</span></span>

## <a name="grantrevoke-access"></a><span data-ttu-id="f689c-315">授與/撤銷存取權</span><span class="sxs-lookup"><span data-stu-id="f689c-315">Grant/revoke access</span></span>
<span data-ttu-id="f689c-316">HDInsight 叢集具有下列 HTTP Web 服務 (所有這些服務都有 RESTful 端點)：</span><span class="sxs-lookup"><span data-stu-id="f689c-316">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="f689c-317">ODBC</span><span class="sxs-lookup"><span data-stu-id="f689c-317">ODBC</span></span>
* <span data-ttu-id="f689c-318">JDBC</span><span class="sxs-lookup"><span data-stu-id="f689c-318">JDBC</span></span>
* <span data-ttu-id="f689c-319">Ambari</span><span class="sxs-lookup"><span data-stu-id="f689c-319">Ambari</span></span>
* <span data-ttu-id="f689c-320">Oozie</span><span class="sxs-lookup"><span data-stu-id="f689c-320">Oozie</span></span>
* <span data-ttu-id="f689c-321">Templeton</span><span class="sxs-lookup"><span data-stu-id="f689c-321">Templeton</span></span>

<span data-ttu-id="f689c-322">預設會授與這些服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="f689c-322">By default, these services are granted for access.</span></span> <span data-ttu-id="f689c-323">您可以使用 [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) 和 [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access) 撤銷/授與存取權。</span><span class="sxs-lookup"><span data-stu-id="f689c-323">You can revoke/grant the access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span></span>

## <a name="find-the-subscription-id"></a><span data-ttu-id="f689c-324">尋找訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="f689c-324">Find the subscription ID</span></span>

<span data-ttu-id="f689c-325">**尋找您的 Azure 訂用帳戶識別碼**</span><span class="sxs-lookup"><span data-stu-id="f689c-325">**To find your Azure subscription IDs**</span></span>

1. <span data-ttu-id="f689c-326">登入[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="f689c-326">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="f689c-327">按一下 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f689c-327">Click **Subscriptions**.</span></span> <span data-ttu-id="f689c-328">每個訂用帳戶都有一個名稱和一個識別碼。</span><span class="sxs-lookup"><span data-stu-id="f689c-328">Each subscription has a name and an ID.</span></span>

<span data-ttu-id="f689c-329">每個叢集都會繫結至一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f689c-329">Each cluster is tied to an Azure subscription.</span></span> <span data-ttu-id="f689c-330">訂用帳戶識別碼會顯示在叢集 [基本資料]  圖格上。</span><span class="sxs-lookup"><span data-stu-id="f689c-330">The subscription ID is shown on the cluster **Essential** tile.</span></span> <span data-ttu-id="f689c-331">請參閱 [列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f689c-331">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-resource-group"></a><span data-ttu-id="f689c-332">尋找資源群組</span><span class="sxs-lookup"><span data-stu-id="f689c-332">Find the resource group</span></span>
<span data-ttu-id="f689c-333">在 Azure Resource Manager 模式中，每個 HDInsight 叢集是隨著 Azure Resource Manager 群組一起建立。</span><span class="sxs-lookup"><span data-stu-id="f689c-333">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span></span> <span data-ttu-id="f689c-334">叢集所屬的 Resource Manager 群組會出現於：</span><span class="sxs-lookup"><span data-stu-id="f689c-334">The Resource Manager group that a cluster belongs to appears in:</span></span>

* <span data-ttu-id="f689c-335">叢集清單含有 [資源群組]  資料行。</span><span class="sxs-lookup"><span data-stu-id="f689c-335">The cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="f689c-336">叢集 [基本資料]  磚。</span><span class="sxs-lookup"><span data-stu-id="f689c-336">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="f689c-337">請參閱 [列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f689c-337">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="f689c-338">尋找預設的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f689c-338">Find the default storage account</span></span>
<span data-ttu-id="f689c-339">每個 HDInsight 叢集都有預設的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f689c-339">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="f689c-340">叢集的預設儲存體帳戶與其金鑰會顯示在 [儲存體帳戶] 之下。</span><span class="sxs-lookup"><span data-stu-id="f689c-340">The default storage account and its keys for a cluster appears under **Storage Accounts**.</span></span> <span data-ttu-id="f689c-341">請參閱 [列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f689c-341">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="run-hive-queries"></a><span data-ttu-id="f689c-342">執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="f689c-342">Run Hive queries</span></span>
<span data-ttu-id="f689c-343">您無法直接從 Azure 入口網站執行 Hive 作業，但您可以使用 Ambari Web UI 上的 Hive 檢視。</span><span class="sxs-lookup"><span data-stu-id="f689c-343">You cannot run Hive job directly from the Azure portal, but you can use the Hive View on Ambari Web UI.</span></span>

<span data-ttu-id="f689c-344">**使用 Ambari Hive 檢視執行 Hive 查詢**</span><span class="sxs-lookup"><span data-stu-id="f689c-344">**To run Hive queries using Ambari Hive View**</span></span>

1. <span data-ttu-id="f689c-345">使用 HDInsight 叢集使用者認證登入 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="f689c-345">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="f689c-346">預設的使用者名稱為 **admin**。URL 是 **https://&lt;HDInsight 叢集名稱>azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="f689c-346">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="f689c-347">開啟 [Hive 檢視]，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="f689c-347">Open Hive View as shown in the following screenshot:</span></span>  

    ![HDInsight Hive 檢視](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. <span data-ttu-id="f689c-349">按一下頂端功能表中的 [查詢]  。</span><span class="sxs-lookup"><span data-stu-id="f689c-349">Click **Query** from the top menu.</span></span>
4. <span data-ttu-id="f689c-350">在 [查詢編輯器] 中輸入 Hive 查詢，然後按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="f689c-350">Enter a Hive query in **Query Editor**, and then click **Execute**.</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="f689c-351">監視工作</span><span class="sxs-lookup"><span data-stu-id="f689c-351">Monitor jobs</span></span>
<span data-ttu-id="f689c-352">請參閱 [使用 Ambari Web UI 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md#monitoring)。</span><span class="sxs-lookup"><span data-stu-id="f689c-352">See [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span></span>

## <a name="browse-files"></a><span data-ttu-id="f689c-353">瀏覽檔案</span><span class="sxs-lookup"><span data-stu-id="f689c-353">Browse files</span></span>
<span data-ttu-id="f689c-354">使用 Azure 入口網站時，您可以瀏覽預設容器的內容。</span><span class="sxs-lookup"><span data-stu-id="f689c-354">Using the Azure portal, you can browse the content of the default container.</span></span>

1. <span data-ttu-id="f689c-355">登入 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f689c-355">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f689c-356">按一下左側功能表中的 [HDInsight 叢集]  以列出現有的叢集。</span><span class="sxs-lookup"><span data-stu-id="f689c-356">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="f689c-357">按一下叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f689c-357">Click the cluster name.</span></span> <span data-ttu-id="f689c-358">如果叢集清單很長，您可以使用頁面頂端的篩選器。</span><span class="sxs-lookup"><span data-stu-id="f689c-358">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="f689c-359">按一下叢集左側功能表中的 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f689c-359">Click **Storage Accounts** from the cluster left menu.</span></span>
5. <span data-ttu-id="f689c-360">按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f689c-360">Click a Storage account.</span></span>
7. <span data-ttu-id="f689c-361">按一下 [blob]  圖格。</span><span class="sxs-lookup"><span data-stu-id="f689c-361">Click the **Blobs** tile.</span></span>
8. <span data-ttu-id="f689c-362">按一下預設容器名稱。</span><span class="sxs-lookup"><span data-stu-id="f689c-362">Click the default container name.</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="f689c-363">監視叢集使用量</span><span class="sxs-lookup"><span data-stu-id="f689c-363">Monitor cluster usage</span></span>
<span data-ttu-id="f689c-364">HDInsight 叢集刀鋒視窗的 [使用量] 區段會顯示以下資訊：訂用帳戶可搭配 HDInsight 使用的核心數目，以及配置給此叢集的核心數目和它們在此叢集中配置給節點的方式。</span><span class="sxs-lookup"><span data-stu-id="f689c-364">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span></span> <span data-ttu-id="f689c-365">請參閱 [列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f689c-365">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f689c-366">若要監視 HDInsight 叢集所提供的服務，您必須使用 Ambari Web 或 Ambari REST API。</span><span class="sxs-lookup"><span data-stu-id="f689c-366">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="f689c-367">如需使用 Ambari 的詳細資訊，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="f689c-367">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="connect-to-a-cluster"></a><span data-ttu-id="f689c-368">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-368">Connect to a cluster</span></span>

* [<span data-ttu-id="f689c-369">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="f689c-369">Use Hive with HDInsight</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
* [<span data-ttu-id="f689c-370">搭配使用 SSH 與 HDInsight</span><span class="sxs-lookup"><span data-stu-id="f689c-370">Use SSH with HDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a><span data-ttu-id="f689c-371">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f689c-371">Next steps</span></span>
<span data-ttu-id="f689c-372">在本文中，您已了解一些基本的系統管理函式。</span><span class="sxs-lookup"><span data-stu-id="f689c-372">In this article, you have learned some basic administative functions.</span></span> <span data-ttu-id="f689c-373">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="f689c-373">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="f689c-374">使用 Azure PowerShell 管理 HDInsight</span><span class="sxs-lookup"><span data-stu-id="f689c-374">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="f689c-375">使用 Azure CLI 管理 HDInsight</span><span class="sxs-lookup"><span data-stu-id="f689c-375">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="f689c-376">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f689c-376">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="f689c-377">在 HDInsight 中使用 Hive</span><span class="sxs-lookup"><span data-stu-id="f689c-377">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f689c-378">在 HDInsight 中使用 Pig</span><span class="sxs-lookup"><span data-stu-id="f689c-378">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f689c-379">在 HDInsight 中使用 Sqoop</span><span class="sxs-lookup"><span data-stu-id="f689c-379">Use Sqoop in HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="f689c-380">開始使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f689c-380">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="f689c-381">Azure HDInsight 提供 Hadoop 的什麼版本？</span><span class="sxs-lookup"><span data-stu-id="f689c-381">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop 命令列"
