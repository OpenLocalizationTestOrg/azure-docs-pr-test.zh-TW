---
title: "使用 Azure 入口網站的 HDInsight 叢集 aaaManage Hadoop |Microsoft 文件"
description: "深入了解如何 toocreate 和管理 HDInsight 叢集使用 hello Azure 入口網站。"
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
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a><span data-ttu-id="349d4-103">透過 hello Azure 入口網站來管理 HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-103">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="349d4-104">使用 hello [Azure 入口網站][azure-portal]，您可以管理在 Azure HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-104">Using hello [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="349d4-105">如需有關管理中使用其他工具的 HDInsight Hadoop 叢集資訊使用 hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="349d4-105">Use hello tab selector for information on managing Hadoop clusters in HDInsight using other tools.</span></span>

<span data-ttu-id="349d4-106">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="349d4-106">**Prerequisites**</span></span>

<span data-ttu-id="349d4-107">在開始這份文件之前，您必須擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="349d4-107">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="349d4-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="349d4-108">**An Azure subscription**.</span></span> <span data-ttu-id="349d4-109">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="349d4-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="open-hello-portal"></a><span data-ttu-id="349d4-110">開啟 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="349d4-110">Open hello portal</span></span>
1. <span data-ttu-id="349d4-111">登入太[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="349d4-111">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="349d4-112">開啟 hello 入口網站之後，您可以：</span><span class="sxs-lookup"><span data-stu-id="349d4-112">After you open hello portal, you can:</span></span>

   * <span data-ttu-id="349d4-113">按一下**新增**從 hello 左側的功能表 toocreate 新叢集：</span><span class="sxs-lookup"><span data-stu-id="349d4-113">Click **New** from hello left menu toocreate a new cluster:</span></span>

       ![新的 HDInsight 叢集按鈕](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * <span data-ttu-id="349d4-115">按一下**HDInsight 叢集**hello 從左側的功能表 toolist hello 現有叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-115">Click **HDInsight Clusters** from hello left menu toolist hello existing clusters</span></span>

       ![Azure 入口網站 HDInsight 叢集按鈕](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       <span data-ttu-id="349d4-117">如果您沒有看到 HDInsight 叢集，按一下 **更多服務**在 hello hello 清單的底部，然後按一下 **HDInsight 叢集**下 hello**智慧 + 分析**一節。</span><span class="sxs-lookup"><span data-stu-id="349d4-117">If you don't see HDInsight cluster, click **More services** on hello bottom of hello list, and then click **HDInsight clusters** under hello **Intelligence + Analytics** section.</span></span>


## <a name="create-clusters"></a><span data-ttu-id="349d4-118">建立叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-118">Create clusters</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="349d4-119">HDInsight 可以與很多 Hadoop 元件搭配使用。</span><span class="sxs-lookup"><span data-stu-id="349d4-119">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="349d4-120">Hello 驗證以及支援 hello 元件清單，請參閱[的 Hadoop 版本是在 Azure HDInsight](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-120">For hello list of hello components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="349d4-121">建立 hello 一般叢集中的資訊，請參閱[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-121">For hello general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="349d4-122">存取控制需求</span><span class="sxs-lookup"><span data-stu-id="349d4-122">Access control requirements</span></span>

<span data-ttu-id="349d4-123">當您建立 HDInsight 叢集時，必須指定 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-123">You must specify an Azure subscription when you create an HDInsight cluster.</span></span> <span data-ttu-id="349d4-124">這個叢集可在新的 Azure 資源群組中建立，或是在現有的資源群組中建立。</span><span class="sxs-lookup"><span data-stu-id="349d4-124">This cluster can be created in either a new Azure Resource group or an existing Resource group.</span></span> <span data-ttu-id="349d4-125">您可以使用下列步驟 tooverify hello 您的權限，來建立 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="349d4-125">You can use hello following steps tooverify your permissions for creating HDInsight clusters:</span></span>

- <span data-ttu-id="349d4-126">toouse 現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="349d4-126">toouse an existing resource group.</span></span>

    1. <span data-ttu-id="349d4-127">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="349d4-127">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="349d4-128">按一下**資源群組**從 hello 左側的功能表 toolist hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="349d4-128">Click **Resource groups** from hello left menu toolist hello resource groups.</span></span>
    3. <span data-ttu-id="349d4-129">按一下您要建立您的 HDInsight 叢集的 toouse hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="349d4-129">Click hello resource group you want toouse for creating your HDInsight cluster.</span></span>
    4. <span data-ttu-id="349d4-130">按一下**存取控制 (IAM)**，並確認您 （或您所屬的群組） 有至少 hello 參與者存取 toohello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="349d4-130">Click **Access control (IAM)**, and verify that you (or a group that you belong to) have at least hello Contributor access toohello resource group.</span></span>

- <span data-ttu-id="349d4-131">toocreate 新的資源群組</span><span class="sxs-lookup"><span data-stu-id="349d4-131">toocreate a new resource group</span></span>

    1. <span data-ttu-id="349d4-132">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="349d4-132">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="349d4-133">按一下**訂用帳戶**hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="349d4-133">Click **Subscription** from hello left menu.</span></span> <span data-ttu-id="349d4-134">它有黃色的鑰匙圖示。</span><span class="sxs-lookup"><span data-stu-id="349d4-134">It has a yellow key icon.</span></span> <span data-ttu-id="349d4-135">您應該會看到訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="349d4-135">You shall see a list of subscriptions.</span></span>
    3. <span data-ttu-id="349d4-136">按一下您將 toocreate 叢集 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-136">Click hello subscription that you use toocreate clusters.</span></span> 
    4. <span data-ttu-id="349d4-137">按一下 [我的權限]。</span><span class="sxs-lookup"><span data-stu-id="349d4-137">Click **My permissions**.</span></span>  <span data-ttu-id="349d4-138">它會顯示您[角色](../active-directory/role-based-access-control-what-is.md#built-in-roles)hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-138">It shows your [role](../active-directory/role-based-access-control-what-is.md#built-in-roles) on hello subscription.</span></span> <span data-ttu-id="349d4-139">您必須至少參與者存取 toocreate HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-139">You need at least Contributor access toocreate HDInsight cluster.</span></span>

<span data-ttu-id="349d4-140">如果您收到 hello NoRegisteredProviderFound 錯誤或 hello MissingSubscriptionRegistration 錯誤，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](../azure-resource-manager/resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-140">If you receive hello NoRegisteredProviderFound error or hello MissingSubscriptionRegistration error, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="349d4-141">列出和顯示叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-141">List and show clusters</span></span>
1. <span data-ttu-id="349d4-142">登入太[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="349d4-142">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="349d4-143">按一下**HDInsight 叢集**hello 從左側的功能表 toolist hello 現有的叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-143">Click **HDInsight Clusters** from hello left menu toolist hello existing clusters.</span></span>
3. <span data-ttu-id="349d4-144">按一下 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="349d4-144">Click hello cluster name.</span></span> <span data-ttu-id="349d4-145">如果 hello 叢集清單很長，您可以使用篩選器上 hello hello 頁面的頂端。</span><span class="sxs-lookup"><span data-stu-id="349d4-145">If hello cluster list is long, you can use filter on hello top of hello page.</span></span>
4. <span data-ttu-id="349d4-146">按一下從 hello 清單 toosee hello 概觀頁面上的叢集：</span><span class="sxs-lookup"><span data-stu-id="349d4-146">Click a cluster from hello list toosee hello overview page:</span></span>

    ![Azure portal HDInsight cluster essentials](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * <span data-ttu-id="349d4-148">**儀表板**： 開啟 hello 叢集儀表板，也就是 Ambari Web 用於以 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-148">**Dashboard**: Opens hello cluster dashboard, which is Ambari Web for Linux-based clusters.</span></span>
    * <span data-ttu-id="349d4-149">**安全殼層**： 顯示 hello 指示 tooconnect toohello 叢集使用安全殼層 (SSH) 連線。</span><span class="sxs-lookup"><span data-stu-id="349d4-149">**Secure Shell**: Shows hello instructions tooconnect toohello cluster using Secure Shell (SSH) connection.</span></span>
    * <span data-ttu-id="349d4-150">**調整叢集**： 可讓您對此叢集的背景工作節點 toochange hello 數。</span><span class="sxs-lookup"><span data-stu-id="349d4-150">**Scale Cluster**: Allows you toochange hello number of worker nodes for this cluster.</span></span>
    * <span data-ttu-id="349d4-151">**刪除**： 刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-151">**Delete**: Deletes hello cluster.</span></span>
    * <span data-ttu-id="349d4-152">**活動記錄檔**︰顯示和查詢活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="349d4-152">**Activity logs**: Show and query activity logs.</span></span>
    * <span data-ttu-id="349d4-153">**存取控制 (IAM)**︰使用角色指派。</span><span class="sxs-lookup"><span data-stu-id="349d4-153">**Access control (IAM)**: Use role assignments.</span></span>  <span data-ttu-id="349d4-154">請參閱[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-154">See [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
    * <span data-ttu-id="349d4-155">**標記**： 可讓您 tooset 索引鍵/值組 toodefine 自訂您的雲端服務的分類。</span><span class="sxs-lookup"><span data-stu-id="349d4-155">**Tags**: Allows you tooset key/value pairs toodefine a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="349d4-156">例如，您可建立名為 **project**的索引鍵，然後使用與特定專案相關聯之所有服務的通用值。</span><span class="sxs-lookup"><span data-stu-id="349d4-156">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
    * <span data-ttu-id="349d4-157">**診斷並解決問題**︰顯示疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="349d4-157">**Diagnose and solve problems**: Display troubleshooting information.</span></span>
    * <span data-ttu-id="349d4-158">**鎖定**： 新增鎖定 tooprevent hello 叢集正在修改或刪除。</span><span class="sxs-lookup"><span data-stu-id="349d4-158">**Locks**: Add lock tooprevent hello cluster being modified or deleted.</span></span>
    * <span data-ttu-id="349d4-159">**自動化指令碼**: hello 叢集的顯示和匯出 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="349d4-159">**Automation script**: Display and export hello Azure Resource Manager template for hello cluster.</span></span> <span data-ttu-id="349d4-160">目前，您可以只匯出 hello 相依的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-160">Currently, you can only export hello dependent Azure storage account.</span></span> <span data-ttu-id="349d4-161">請參閱[使用 Azure Resource Manager 範本在 HDInsight 中建立 Linux 型 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-161">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>
    * <span data-ttu-id="349d4-162">**快速啟動**：顯示可協助您開始使用 HDInsight 的資訊。</span><span class="sxs-lookup"><span data-stu-id="349d4-162">**Quick Start**:  Displays information that helps you get started using HDInsight.</span></span>
    * <span data-ttu-id="349d4-163">**適用於 HDInsight 的工具**：HDInsight 相關工具的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="349d4-163">**Tools for HDInsight**: Help information for HDInsight related tools.</span></span>
    * <span data-ttu-id="349d4-164">**叢集登入**： 顯示 hello 叢集登入資訊。</span><span class="sxs-lookup"><span data-stu-id="349d4-164">**Cluster Login**: Display hello cluster login information.</span></span>
    * <span data-ttu-id="349d4-165">**訂用帳戶核心使用量**： 顯示 hello 訂用帳戶的使用和可用的核心。</span><span class="sxs-lookup"><span data-stu-id="349d4-165">**Subscription Core Usage**: Display hello used and available cores for your subscription.</span></span>
    * <span data-ttu-id="349d4-166">**調整叢集**： 增減 hello 叢集背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="349d4-166">**Scale Cluster**: Increase and decrease hello number of cluster worker nodes.</span></span> <span data-ttu-id="349d4-167">請參閱[調整叢集](hdinsight-administer-use-management-portal.md#scale-clusters)。</span><span class="sxs-lookup"><span data-stu-id="349d4-167">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span></span>
    * <span data-ttu-id="349d4-168">**安全殼層**： 顯示 hello 指示 tooconnect toohello 叢集使用安全殼層 (SSH) 連線。</span><span class="sxs-lookup"><span data-stu-id="349d4-168">**Secure Shell**: Shows hello instructions tooconnect toohello cluster using Secure Shell (SSH) connection.</span></span> <span data-ttu-id="349d4-169">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-169">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
    * <span data-ttu-id="349d4-170">**HDInsight 合作夥伴**： 新增/移除 hello 目前的 HDInsight 合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="349d4-170">**HDInsight Partner**: Add/remove hello current HDInsight Partner.</span></span>
    * <span data-ttu-id="349d4-171">**外部中繼存放區**： 檢視 hello Hive 和 Oozie 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="349d4-171">**External Metastores**: View hello Hive and Oozie metastores.</span></span> <span data-ttu-id="349d4-172">只能在 hello 叢集建立程序期間設定 hello 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="349d4-172">hello metastores can only be configured during hello cluster creation process.</span></span> <span data-ttu-id="349d4-173">請參閱[使用 Hive/Oozie 中繼存放區](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore)。</span><span class="sxs-lookup"><span data-stu-id="349d4-173">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span></span>
    * <span data-ttu-id="349d4-174">**編寫指令碼動作**： 執行撞 hello 叢集上的指令碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-174">**Script Actions**: Run Bash scripts on hello cluster.</span></span> <span data-ttu-id="349d4-175">請參閱 [使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-175">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    * <span data-ttu-id="349d4-176">**應用程式**：新增/移除 HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="349d4-176">**Applications**: Add/remove HDInsight applications.</span></span>  <span data-ttu-id="349d4-177">請參閱[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-177">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
    * <span data-ttu-id="349d4-178">**屬性**： 檢視 hello 叢集內容。</span><span class="sxs-lookup"><span data-stu-id="349d4-178">**Properties**: View hello cluster properties.</span></span>
    * <span data-ttu-id="349d4-179">**儲存體帳戶**： 檢視 hello 儲存體帳戶和 hello 機碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-179">**Storage accounts**: View hello storage accounts and hello keys.</span></span> <span data-ttu-id="349d4-180">hello 叢集建立程序期間，會設定 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-180">hello storage accounts are configured during hello cluster creation process.</span></span>
    * <span data-ttu-id="349d4-181">**叢集 AAD 身分識別**：</span><span class="sxs-lookup"><span data-stu-id="349d4-181">**Cluster AAD Identity**:</span></span>
    * <span data-ttu-id="349d4-182">**新的支援要求**： 可讓您 toocreate 支援票證，向 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="349d4-182">**New support request**: Allows you toocreate a support ticket with Microsoft support.</span></span>
    
6. <span data-ttu-id="349d4-183">按一下 [屬性] ：</span><span class="sxs-lookup"><span data-stu-id="349d4-183">Click **Properties**:</span></span>

    <span data-ttu-id="349d4-184">hello 屬性如下：</span><span class="sxs-lookup"><span data-stu-id="349d4-184">hello properties are:</span></span>

   * <span data-ttu-id="349d4-185">**主機名稱**：叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="349d4-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="349d4-186">**叢集 URL**。</span><span class="sxs-lookup"><span data-stu-id="349d4-186">**Cluster URL**.</span></span> <span data-ttu-id="349d4-187">hello hello Ambari web 介面的 URL。</span><span class="sxs-lookup"><span data-stu-id="349d4-187">hello URL for hello Ambari web interface.</span></span>
   * <span data-ttu-id="349d4-188">**狀態**：包括Aborted、Accepted、ClusterStorageProvisioned、AzureVMConfiguration、HDInsightConfiguration、Operational、Running、Error、Deleting、Deleted、Timedout、DeleteQueued、DeleteTimedout、DeleteError、PatchQueued、CertRolloverQueued、ResizeQueued、ClusterCustomization</span><span class="sxs-lookup"><span data-stu-id="349d4-188">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="349d4-189">**區域**：Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="349d4-189">**Region**: Azure location.</span></span> <span data-ttu-id="349d4-190">如需支援的 Azure 位置的清單，請參閱 hello**區域**下拉式清單方塊上的[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="349d4-190">For a list of supported Azure locations, see hello **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="349d4-191">**建立日期**。</span><span class="sxs-lookup"><span data-stu-id="349d4-191">**Date created**.</span></span>
   * <span data-ttu-id="349d4-192">**作業系統**：**Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="349d4-192">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="349d4-193">**類型**：Hadoop、HBase、Storm、Spark。</span><span class="sxs-lookup"><span data-stu-id="349d4-193">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="349d4-194">**版本**。</span><span class="sxs-lookup"><span data-stu-id="349d4-194">**Version**.</span></span> <span data-ttu-id="349d4-195">請參閱 [HDInsight 版本](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="349d4-195">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="349d4-196">**訂用帳戶**︰訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="349d4-196">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="349d4-197">**預設的資料來源**: hello 預設叢集檔案系統。</span><span class="sxs-lookup"><span data-stu-id="349d4-197">**Default data source**: hello default cluster file system.</span></span>
   * <span data-ttu-id="349d4-198">**背景工作節點**。</span><span class="sxs-lookup"><span data-stu-id="349d4-198">**Worker nodes size**.</span></span>
   * <span data-ttu-id="349d4-199">**前端節點大小**。</span><span class="sxs-lookup"><span data-stu-id="349d4-199">**Head node size**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="349d4-200">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-200">Delete clusters</span></span>
<span data-ttu-id="349d4-201">正在刪除叢集不會刪除 hello 預設儲存體帳戶或任何連結儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-201">Deleting a cluster does not delete hello default storage account or any linked storage accounts.</span></span> <span data-ttu-id="349d4-202">您可以使用，以重新建立 hello 叢集 hello 相同的儲存體帳戶和 hello 相同中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="349d4-202">You can re-create hello cluster by using hello same storage accounts and hello same metastores.</span></span> <span data-ttu-id="349d4-203">它是您重新建立 hello 叢集的使用者 toouse 建議新的預設 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="349d4-203">It is recommended toouse a new default Blob container when you re-create hello cluster.</span></span>

1. <span data-ttu-id="349d4-204">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="349d4-204">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="349d4-205">按一下**HDInsight 叢集**hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="349d4-205">Click **HDInsight Clusters** from hello left menu.</span></span> <span data-ttu-id="349d4-206">如果您沒有看到 [HDInsight 叢集]，可先按一下 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="349d4-206">If you don't see **HDInsight Clusters**, click **More services** first.</span></span>
3. <span data-ttu-id="349d4-207">按一下您想 toodelete hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-207">Click hello cluster that you want toodelete.</span></span>
4. <span data-ttu-id="349d4-208">按一下**刪除**從 hello 上方功能表中，然後再遵循 hello 的指示。</span><span class="sxs-lookup"><span data-stu-id="349d4-208">Click **Delete** from hello top menu, and then follow hello instructions.</span></span>

<span data-ttu-id="349d4-209">另請參閱 [暫停/關閉叢集](#pauseshut-down-clusters)。</span><span class="sxs-lookup"><span data-stu-id="349d4-209">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="349d4-210">新增其他儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="349d4-210">Add additional storage accounts</span></span>

<span data-ttu-id="349d4-211">建立叢集之後，您可以新增其他 Azure 儲存體帳戶和 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-211">You can add additional Azure Storage accounts and Azure Data Lake Store accounts after a cluster is created.</span></span> <span data-ttu-id="349d4-212">如需詳細資訊，請參閱[新增額外的儲存體帳戶 tooHDInsight](./hdinsight-hadoop-add-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-212">For more information, see [Add additional storage accounts tooHDInsight](./hdinsight-hadoop-add-storage.md).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="349d4-213">調整叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-213">Scale clusters</span></span>
<span data-ttu-id="349d4-214">hello 叢集擴充功能可讓您在 Azure HDInsight 中執行而不需要 toore 叢集所用的背景工作節點 toochange hello 數-建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-214">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="349d4-215">只支援使用 HDInsight 3.1.3 版或更高版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-215">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="349d4-216">如果您不確定您的叢集 hello 版本，您可以檢查 hello 屬性頁面。</span><span class="sxs-lookup"><span data-stu-id="349d4-216">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="349d4-217">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="349d4-217">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="349d4-218">hello 變更造成的影響 hello 支援 HDInsight 叢集的每種類型的資料節點數目：</span><span class="sxs-lookup"><span data-stu-id="349d4-218">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="349d4-219">Hadoop</span><span class="sxs-lookup"><span data-stu-id="349d4-219">Hadoop</span></span>

    <span data-ttu-id="349d4-220">您可以順暢地增加 hello Hadoop 叢集中執行而不會影響任何暫止或執行工作的背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="349d4-220">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="349d4-221">Hello 作業正在進行時，也可以提交新的作業。</span><span class="sxs-lookup"><span data-stu-id="349d4-221">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="349d4-222">使 hello 叢集一律會保持在運作狀態，是依正常程序處理中縮放作業失敗。</span><span class="sxs-lookup"><span data-stu-id="349d4-222">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="349d4-223">當在 Hadoop 叢集縮小藉由減少 hello 資料節點數時，部分 hello hello 叢集中的服務會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="349d4-223">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="349d4-224">所有執行和暫止的工作 toofail hello hello 調整大小作業完成時，會導致此行為。</span><span class="sxs-lookup"><span data-stu-id="349d4-224">This behavior causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="349d4-225">您可以不過，再重新送出 hello 工作一旦 hello 作業已完成。</span><span class="sxs-lookup"><span data-stu-id="349d4-225">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="349d4-226">HBase</span><span class="sxs-lookup"><span data-stu-id="349d4-226">HBase</span></span>

    <span data-ttu-id="349d4-227">順暢地，您可以新增或移除節點 tooyour HBase 叢集正在執行時。</span><span class="sxs-lookup"><span data-stu-id="349d4-227">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="349d4-228">完成 hello 調整大小作業的幾分鐘內自動平衡地區的伺服器。</span><span class="sxs-lookup"><span data-stu-id="349d4-228">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="349d4-229">不過，您就可以手動平衡 hello 地區的伺服器登入以 toohello 叢集前端節點的叢集和執行 hello 的命令提示字元視窗中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="349d4-229">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="349d4-230">如需有關使用 hello HBase 殼層的詳細資訊，請參閱]</span><span class="sxs-lookup"><span data-stu-id="349d4-230">For more information on using hello HBase shell, see []</span></span>
* <span data-ttu-id="349d4-231">Storm</span><span class="sxs-lookup"><span data-stu-id="349d4-231">Storm</span></span>

    <span data-ttu-id="349d4-232">順暢地，您可以新增或移除在執行時的資料節點 tooyour Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-232">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="349d4-233">但是 hello 調整大小作業順利完成之後, 您將需要 toorebalance hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="349d4-233">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="349d4-234">您可以使用兩種方式來完成重新平衡作業：</span><span class="sxs-lookup"><span data-stu-id="349d4-234">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="349d4-235">Storm Web UI</span><span class="sxs-lookup"><span data-stu-id="349d4-235">Storm web UI</span></span>
  * <span data-ttu-id="349d4-236">命令列介面 (CLI) 工具</span><span class="sxs-lookup"><span data-stu-id="349d4-236">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="349d4-237">請參閱 toohello [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="349d4-237">Refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="349d4-238">hello Storm web UI 是在 hello HDInsight 叢集上使用：</span><span class="sxs-lookup"><span data-stu-id="349d4-238">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![HDInsight Storm 調整重新平衡](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="349d4-240">以下是範例如何 toouse hello CLI 命令 toorebalance hello Storm 拓撲：</span><span class="sxs-lookup"><span data-stu-id="349d4-240">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="349d4-241">**tooscale 叢集**</span><span class="sxs-lookup"><span data-stu-id="349d4-241">**tooscale clusters**</span></span>

1. <span data-ttu-id="349d4-242">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="349d4-242">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="349d4-243">按一下**HDInsight 叢集**hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="349d4-243">Click **HDInsight Clusters** from hello left menu.</span></span>
3. <span data-ttu-id="349d4-244">按一下您想要 tooscale hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-244">Click hello cluster you want tooscale.</span></span>
3. <span data-ttu-id="349d4-245">按一下 [調整叢集]。</span><span class="sxs-lookup"><span data-stu-id="349d4-245">Click **Scale Cluster**.</span></span>
4. <span data-ttu-id="349d4-246">輸入 **背景工作節點的數目**。</span><span class="sxs-lookup"><span data-stu-id="349d4-246">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="349d4-247">hello hello 叢集節點數目限制會因 Azure 訂用帳戶而異。</span><span class="sxs-lookup"><span data-stu-id="349d4-247">hello limit on hello number of cluster nodes varies among Azure subscriptions.</span></span> <span data-ttu-id="349d4-248">您可以連絡帳務支援 tooincrease hello 限制。</span><span class="sxs-lookup"><span data-stu-id="349d4-248">You can contact billing support tooincrease hello limit.</span></span>  <span data-ttu-id="349d4-249">hello 成本資訊會反映您所做的節點 toohello 數目的 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="349d4-249">hello cost information reflects hello changes you have made toohello number of nodes.</span></span>

    ![HDInsight hadoop hbase storm spark scale](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="349d4-251">暫停/關閉叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-251">Pause/shut down clusters</span></span>

<span data-ttu-id="349d4-252">大部分 Hadoop 工作是只會偶爾執行的批次工作。</span><span class="sxs-lookup"><span data-stu-id="349d4-252">Most of Hadoop jobs are batch jobs that are only run occasionally.</span></span> <span data-ttu-id="349d4-253">對於大多數的 Hadoop 叢集有長時間的過 hello 叢集不正進行處理。</span><span class="sxs-lookup"><span data-stu-id="349d4-253">For most Hadoop clusters, there are large periods of time that hello cluster is not being used for processing.</span></span> <span data-ttu-id="349d4-254">利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。</span><span class="sxs-lookup"><span data-stu-id="349d4-254">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="349d4-255">您也需支付 HDInsight 叢集的費用 (即使未使用)。</span><span class="sxs-lookup"><span data-stu-id="349d4-255">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="349d4-256">由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。</span><span class="sxs-lookup"><span data-stu-id="349d4-256">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span>

<span data-ttu-id="349d4-257">有許多方法，您可以程式設計 hello 程序：</span><span class="sxs-lookup"><span data-stu-id="349d4-257">There are many ways you can program hello process:</span></span>

* <span data-ttu-id="349d4-258">使用 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="349d4-258">User Azure Data Factory.</span></span> <span data-ttu-id="349d4-259">如需建立隨選 HDInsight 連結服務，請參閱 [使用 Azure Data Factory 在 HDInsight 中建立 Linux 型隨選 Handooop 叢集](hdinsight-hadoop-create-linux-clusters-adf.md) 。</span><span class="sxs-lookup"><span data-stu-id="349d4-259">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span></span>
* <span data-ttu-id="349d4-260">使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="349d4-260">Use Azure PowerShell.</span></span>  <span data-ttu-id="349d4-261">請參閱 [分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-261">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="349d4-262">使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="349d4-262">Use Azure CLI.</span></span> <span data-ttu-id="349d4-263">請參閱 [使用 Azure CLI 管理 HDInsight 叢集](hdinsight-administer-use-command-line.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-263">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="349d4-264">使用 HDInsight .NET SDK。</span><span class="sxs-lookup"><span data-stu-id="349d4-264">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="349d4-265">請參閱 [提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-265">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="349d4-266">Hello 定價資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="349d4-266">For hello pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="349d4-267">請參閱 toodelete hello 入口網站中，從叢集[刪除叢集](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="349d4-267">toodelete a cluster from hello Portal, see [Delete clusters](#delete-clusters)</span></span>


## <a name="upgrade-clusters"></a><span data-ttu-id="349d4-268">升級叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-268">Upgrade clusters</span></span>

<span data-ttu-id="349d4-269">請參閱[升級 HDInsight 叢集 tooa 較新版本](./hdinsight-upgrade-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-269">See [Upgrade HDInsight cluster tooa newer version](./hdinsight-upgrade-cluster.md).</span></span>

## <a name="change-passwords"></a><span data-ttu-id="349d4-270">變更密碼</span><span class="sxs-lookup"><span data-stu-id="349d4-270">Change passwords</span></span>
<span data-ttu-id="349d4-271">HDInsight 叢集可以有兩個使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-271">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="349d4-272">（也稱為 hello HDInsight 叢集的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="349d4-272">hello HDInsight cluster user account (A.K.A.</span></span> <span data-ttu-id="349d4-273">HTTP 使用者帳戶） 以及 hello 建立程序期間建立 hello SSH 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-273">HTTP user account) and hello SSH user account are created during hello creation process.</span></span> <span data-ttu-id="349d4-274">您可以使用 hello Ambari web UI toochange hello 叢集使用者的帳戶使用者名稱和密碼，以及指令碼動作 toochange hello SSH 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="349d4-274">You can use hello Ambari web UI toochange hello cluster user account username and password, and script actions toochange hello SSH user account</span></span>

### <a name="change-hello-cluster-user-password"></a><span data-ttu-id="349d4-275">變更 hello 叢集使用者密碼</span><span class="sxs-lookup"><span data-stu-id="349d4-275">Change hello cluster user password</span></span>
<span data-ttu-id="349d4-276">您可以使用 hello Ambari Web UI toochange hello 叢集使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-276">You can use hello Ambari Web UI toochange hello Cluster user password.</span></span> <span data-ttu-id="349d4-277">toolog tooAmbari 中的，您必須使用 hello 現有叢集使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-277">toolog in tooAmbari, you must use hello existing cluster username and password.</span></span>

> [!NOTE]
> <span data-ttu-id="349d4-278">變更 hello 叢集使用者 (admin) 密碼可能會導致動作執行針對這個叢集 toofail 指令碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-278">Changing hello cluster user (admin) password may cause script actions ran against this cluster toofail.</span></span> <span data-ttu-id="349d4-279">如果您有任何目標背景工作角色節點的保存的指令碼動作，這些指令碼可能會失敗，當您新增節點 toohello 叢集透過調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="349d4-279">If you have any persisted script actions that target worker nodes, these scripts may fail when you add nodes toohello cluster through resize operations.</span></span> <span data-ttu-id="349d4-280">如需指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="349d4-280">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="349d4-281">登入 toohello Ambari Web UI 使用 hello HDInsight 叢集的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="349d4-281">Sign in toohello Ambari Web UI using hello HDInsight cluster user credentials.</span></span> <span data-ttu-id="349d4-282">hello 預設使用者名稱是**admin**。 URL 是的 hello **https://&lt;HDInsight 叢集名稱 >.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="349d4-282">hello default username is **admin**. hello URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="349d4-283">按一下**Admin**從 hello 上方的功能表，然後按一下 「 管理 Ambari"。</span><span class="sxs-lookup"><span data-stu-id="349d4-283">Click **Admin** from hello top menu, and then click "Manage Ambari".</span></span>
3. <span data-ttu-id="349d4-284">從 hello 左窗格中，按一下 **使用者**。</span><span class="sxs-lookup"><span data-stu-id="349d4-284">From hello left menu, click **Users**.</span></span>
4. <span data-ttu-id="349d4-285">按一下 Admin 。</span><span class="sxs-lookup"><span data-stu-id="349d4-285">Click **Admin**.</span></span>
5. <span data-ttu-id="349d4-286">按一下 [變更密碼] 。</span><span class="sxs-lookup"><span data-stu-id="349d4-286">Click **Change Password**.</span></span>

<span data-ttu-id="349d4-287">Ambari 然後變更 hello hello 叢集中所有節點上的密碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-287">Ambari then changes hello password on all nodes in hello cluster.</span></span>

### <a name="change-hello-ssh-user-password"></a><span data-ttu-id="349d4-288">變更 hello SSH 使用者密碼</span><span class="sxs-lookup"><span data-stu-id="349d4-288">Change hello SSH user password</span></span>
1. <span data-ttu-id="349d4-289">使用文字編輯器中，儲存為檔案命名為下列文字的 hello **changepassword.sh**。</span><span class="sxs-lookup"><span data-stu-id="349d4-289">Using a text editor, save hello following text as a file named **changepassword.sh**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="349d4-290">您必須使用 LF 做 hello 行尾結束符號的編輯器。</span><span class="sxs-lookup"><span data-stu-id="349d4-290">You must use an editor that uses LF as hello line ending.</span></span> <span data-ttu-id="349d4-291">如果 hello 編輯器使用 CRLF，然後 hello 指令碼無法運作。</span><span class="sxs-lookup"><span data-stu-id="349d4-291">If hello editor uses CRLF, then hello script does not work.</span></span>
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. <span data-ttu-id="349d4-292">上傳 hello 檔案 tooa 存取儲存體位置可以是從 HDInsight 使用 HTTP 或 HTTPS 位址。</span><span class="sxs-lookup"><span data-stu-id="349d4-292">Upload hello file tooa storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span></span> <span data-ttu-id="349d4-293">例如，OneDrive 或 Azure Blob 儲存體這類的公用檔案存放區。</span><span class="sxs-lookup"><span data-stu-id="349d4-293">For example, a public file store such as OneDrive or Azure Blob storage.</span></span> <span data-ttu-id="349d4-294">儲存 hello URI （HTTP 或 HTTPS 位址） toohello 檔案，因為 hello 下一個步驟中需要此 URI。</span><span class="sxs-lookup"><span data-stu-id="349d4-294">Save hello URI (HTTP or HTTPS address) toohello file, as this URI is needed in hello next step.</span></span>
3. <span data-ttu-id="349d4-295">從 hello Azure 入口網站，按一下  **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="349d4-295">From hello Azure portal, click **HDInsight Clusters**.</span></span>
4. <span data-ttu-id="349d4-296">按一下您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-296">Click your HDInsight cluster.</span></span>
4. <span data-ttu-id="349d4-297">按一下 [指令碼動作]。</span><span class="sxs-lookup"><span data-stu-id="349d4-297">Click **Script Actions**.</span></span>
4. <span data-ttu-id="349d4-298">從 hello**指令碼動作**刀鋒視窗中，選取**提交新**。</span><span class="sxs-lookup"><span data-stu-id="349d4-298">From hello **Script Actions** blade, select **Submit New**.</span></span> <span data-ttu-id="349d4-299">當 hello**送出指令碼動作**刀鋒視窗中出現，請輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="349d4-299">When hello **Submit script action** blade appears, enter hello following information:</span></span>

   | <span data-ttu-id="349d4-300">欄位</span><span class="sxs-lookup"><span data-stu-id="349d4-300">Field</span></span> | <span data-ttu-id="349d4-301">值</span><span class="sxs-lookup"><span data-stu-id="349d4-301">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="349d4-302">Name</span><span class="sxs-lookup"><span data-stu-id="349d4-302">Name</span></span> |<span data-ttu-id="349d4-303">變更 SSH 密碼</span><span class="sxs-lookup"><span data-stu-id="349d4-303">Change ssh password</span></span> |
   | <span data-ttu-id="349d4-304">Bash 指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="349d4-304">Bash script URI</span></span> |<span data-ttu-id="349d4-305">hello URI toohello changepassword.sh 檔案</span><span class="sxs-lookup"><span data-stu-id="349d4-305">hello URI toohello changepassword.sh file</span></span> |
   | <span data-ttu-id="349d4-306">節點 (前端、背景工作、Nimbus、監督員、Zookeeper 等)</span><span class="sxs-lookup"><span data-stu-id="349d4-306">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span></span> |<span data-ttu-id="349d4-307">✓ 針對列出的所有節點類型</span><span class="sxs-lookup"><span data-stu-id="349d4-307">✓ for all node types listed</span></span> |
   | <span data-ttu-id="349d4-308">參數</span><span class="sxs-lookup"><span data-stu-id="349d4-308">Parameters</span></span> |<span data-ttu-id="349d4-309">輸入 hello SSH 使用者名稱，然後 hello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-309">Enter hello SSH user name and then hello new password.</span></span> <span data-ttu-id="349d4-310">應該要有一個 hello 使用者名稱和密碼 hello 之間的空格。</span><span class="sxs-lookup"><span data-stu-id="349d4-310">There should be one space between hello user name and hello password.</span></span> |
   | <span data-ttu-id="349d4-311">保存這個指令碼動作...</span><span class="sxs-lookup"><span data-stu-id="349d4-311">Persist this script action ...</span></span> |<span data-ttu-id="349d4-312">不選取此欄位。</span><span class="sxs-lookup"><span data-stu-id="349d4-312">Leave this field unchecked.</span></span> |
5. <span data-ttu-id="349d4-313">選取**建立**tooapply hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-313">Select **Create** tooapply hello script.</span></span> <span data-ttu-id="349d4-314">一旦 hello 指令碼完成時，您就可以 tooconnect toohello 叢集使用 SSH 使用 hello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-314">Once hello script finishes, you are able tooconnect toohello cluster using SSH with hello new password.</span></span>

## <a name="grantrevoke-access"></a><span data-ttu-id="349d4-315">授與/撤銷存取權</span><span class="sxs-lookup"><span data-stu-id="349d4-315">Grant/revoke access</span></span>
<span data-ttu-id="349d4-316">HDInsight 叢集都有下列 （所有這些服務有 RESTful 端點） 的 HTTP web 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="349d4-316">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="349d4-317">ODBC</span><span class="sxs-lookup"><span data-stu-id="349d4-317">ODBC</span></span>
* <span data-ttu-id="349d4-318">JDBC</span><span class="sxs-lookup"><span data-stu-id="349d4-318">JDBC</span></span>
* <span data-ttu-id="349d4-319">Ambari</span><span class="sxs-lookup"><span data-stu-id="349d4-319">Ambari</span></span>
* <span data-ttu-id="349d4-320">Oozie</span><span class="sxs-lookup"><span data-stu-id="349d4-320">Oozie</span></span>
* <span data-ttu-id="349d4-321">Templeton</span><span class="sxs-lookup"><span data-stu-id="349d4-321">Templeton</span></span>

<span data-ttu-id="349d4-322">預設會授與這些服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="349d4-322">By default, these services are granted for access.</span></span> <span data-ttu-id="349d4-323">您可以撤銷/授與存取權來使用 hello [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster)和[Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access)。</span><span class="sxs-lookup"><span data-stu-id="349d4-323">You can revoke/grant hello access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span></span>

## <a name="find-hello-subscription-id"></a><span data-ttu-id="349d4-324">尋找 hello 訂用帳戶 ID</span><span class="sxs-lookup"><span data-stu-id="349d4-324">Find hello subscription ID</span></span>

<span data-ttu-id="349d4-325">**toofind 您 Azure 訂用帳戶 Id**</span><span class="sxs-lookup"><span data-stu-id="349d4-325">**toofind your Azure subscription IDs**</span></span>

1. <span data-ttu-id="349d4-326">登入 toohello[入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="349d4-326">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="349d4-327">按一下 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="349d4-327">Click **Subscriptions**.</span></span> <span data-ttu-id="349d4-328">每個訂用帳戶都有一個名稱和一個識別碼。</span><span class="sxs-lookup"><span data-stu-id="349d4-328">Each subscription has a name and an ID.</span></span>

<span data-ttu-id="349d4-329">每個叢集是繫結的 tooan Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-329">Each cluster is tied tooan Azure subscription.</span></span> <span data-ttu-id="349d4-330">hello 訂用帳戶 ID 會顯示 hello 叢集**基本**磚。</span><span class="sxs-lookup"><span data-stu-id="349d4-330">hello subscription ID is shown on hello cluster **Essential** tile.</span></span> <span data-ttu-id="349d4-331">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="349d4-331">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-hello-resource-group"></a><span data-ttu-id="349d4-332">找不到 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="349d4-332">Find hello resource group</span></span>
<span data-ttu-id="349d4-333">在 hello Azure Resource Manager 模式中，每個 HDInsight 叢集建立 Azure 資源管理員群組。</span><span class="sxs-lookup"><span data-stu-id="349d4-333">In hello Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span></span> <span data-ttu-id="349d4-334">叢集所屬 tooappears 中的 hello 資源管理員群組：</span><span class="sxs-lookup"><span data-stu-id="349d4-334">hello Resource Manager group that a cluster belongs tooappears in:</span></span>

* <span data-ttu-id="349d4-335">hello 叢集清單有**資源群組**資料行。</span><span class="sxs-lookup"><span data-stu-id="349d4-335">hello cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="349d4-336">叢集 [基本資料]  磚。</span><span class="sxs-lookup"><span data-stu-id="349d4-336">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="349d4-337">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="349d4-337">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="349d4-338">找不到 hello 預設儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="349d4-338">Find hello default storage account</span></span>
<span data-ttu-id="349d4-339">每個 HDInsight 叢集都有預設的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="349d4-339">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="349d4-340">叢集會顯示在 hello 預設儲存體帳戶，而且其索引鍵**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="349d4-340">hello default storage account and its keys for a cluster appears under **Storage Accounts**.</span></span> <span data-ttu-id="349d4-341">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="349d4-341">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="run-hive-queries"></a><span data-ttu-id="349d4-342">執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="349d4-342">Run Hive queries</span></span>
<span data-ttu-id="349d4-343">您無法直接從 hello Azure 入口網站執行 Hive 工作，但是您可以使用 hello Ambari Web UI 上的登錄區的檢視。</span><span class="sxs-lookup"><span data-stu-id="349d4-343">You cannot run Hive job directly from hello Azure portal, but you can use hello Hive View on Ambari Web UI.</span></span>

<span data-ttu-id="349d4-344">**使用 Ambari Hive 檢視 toorun Hive 查詢**</span><span class="sxs-lookup"><span data-stu-id="349d4-344">**toorun Hive queries using Ambari Hive View**</span></span>

1. <span data-ttu-id="349d4-345">登入 toohello Ambari Web UI 使用 hello HDInsight 叢集的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="349d4-345">Sign in toohello Ambari Web UI using hello HDInsight cluster user credentials.</span></span> <span data-ttu-id="349d4-346">hello 預設使用者名稱是**admin**。 URL 是的 hello **https://&lt;HDInsight 叢集名稱 >.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="349d4-346">hello default username is **admin**. hello URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="349d4-347">開啟登錄區的檢視，hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="349d4-347">Open Hive View as shown in hello following screenshot:</span></span>  

    ![HDInsight Hive 檢視](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. <span data-ttu-id="349d4-349">按一下**查詢**從 hello 上方的功能表。</span><span class="sxs-lookup"><span data-stu-id="349d4-349">Click **Query** from hello top menu.</span></span>
4. <span data-ttu-id="349d4-350">在 查詢編輯器 中輸入 Hive 查詢，然後按一下執行。</span><span class="sxs-lookup"><span data-stu-id="349d4-350">Enter a Hive query in **Query Editor**, and then click **Execute**.</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="349d4-351">監視工作</span><span class="sxs-lookup"><span data-stu-id="349d4-351">Monitor jobs</span></span>
<span data-ttu-id="349d4-352">請參閱[管理 HDInsight 叢集使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring)。</span><span class="sxs-lookup"><span data-stu-id="349d4-352">See [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span></span>

## <a name="browse-files"></a><span data-ttu-id="349d4-353">瀏覽檔案</span><span class="sxs-lookup"><span data-stu-id="349d4-353">Browse files</span></span>
<span data-ttu-id="349d4-354">使用 hello Azure 入口網站，您可以瀏覽 hello 的 hello 預設容器的內容。</span><span class="sxs-lookup"><span data-stu-id="349d4-354">Using hello Azure portal, you can browse hello content of hello default container.</span></span>

1. <span data-ttu-id="349d4-355">登入太[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="349d4-355">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="349d4-356">按一下**HDInsight 叢集**hello 從左側的功能表 toolist hello 現有的叢集。</span><span class="sxs-lookup"><span data-stu-id="349d4-356">Click **HDInsight Clusters** from hello left menu toolist hello existing clusters.</span></span>
3. <span data-ttu-id="349d4-357">按一下 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="349d4-357">Click hello cluster name.</span></span> <span data-ttu-id="349d4-358">如果 hello 叢集清單很長，您可以使用篩選器上 hello hello 頁面的頂端。</span><span class="sxs-lookup"><span data-stu-id="349d4-358">If hello cluster list is long, you can use filter on hello top of hello page.</span></span>
4. <span data-ttu-id="349d4-359">按一下**儲存體帳戶**hello 叢集左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="349d4-359">Click **Storage Accounts** from hello cluster left menu.</span></span>
5. <span data-ttu-id="349d4-360">按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="349d4-360">Click a Storage account.</span></span>
7. <span data-ttu-id="349d4-361">按一下 hello **Blob**磚。</span><span class="sxs-lookup"><span data-stu-id="349d4-361">Click hello **Blobs** tile.</span></span>
8. <span data-ttu-id="349d4-362">按一下 hello 預設容器名稱。</span><span class="sxs-lookup"><span data-stu-id="349d4-362">Click hello default container name.</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="349d4-363">監視叢集使用量</span><span class="sxs-lookup"><span data-stu-id="349d4-363">Monitor cluster usage</span></span>
<span data-ttu-id="349d4-364">hello**使用量**hello HDInsight 叢集刀鋒視窗的區段會顯示 hello 核心可用 tooyour HDInsight，搭配使用的訂用帳戶數目，以及 hello toothis 叢集以及其同時配置的核心數目的相關資訊配置給 hello 此叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="349d4-364">hello **Usage** section of hello HDInsight cluster blade displays information about hello number of cores available tooyour subscription for use with HDInsight, as well as hello number of cores allocated toothis cluster and how they are allocated for hello nodes within this cluster.</span></span> <span data-ttu-id="349d4-365">請參閱[列出和顯示叢集](#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="349d4-365">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="349d4-366">toomonitor hello 服務提供 hello HDInsight 叢集，您必須使用 Ambari Web 或 hello Ambari REST API。</span><span class="sxs-lookup"><span data-stu-id="349d4-366">toomonitor hello services provided by hello HDInsight cluster, you must use Ambari Web or hello Ambari REST API.</span></span> <span data-ttu-id="349d4-367">如需使用 Ambari 的詳細資訊，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="349d4-367">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="connect-tooa-cluster"></a><span data-ttu-id="349d4-368">Tooa 叢集連線</span><span class="sxs-lookup"><span data-stu-id="349d4-368">Connect tooa cluster</span></span>

* [<span data-ttu-id="349d4-369">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="349d4-369">Use Hive with HDInsight</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
* [<span data-ttu-id="349d4-370">搭配使用 SSH 與 HDInsight</span><span class="sxs-lookup"><span data-stu-id="349d4-370">Use SSH with HDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a><span data-ttu-id="349d4-371">後續步驟</span><span class="sxs-lookup"><span data-stu-id="349d4-371">Next steps</span></span>
<span data-ttu-id="349d4-372">在本文中，您已了解一些基本的系統管理函式。</span><span class="sxs-lookup"><span data-stu-id="349d4-372">In this article, you have learned some basic administative functions.</span></span> <span data-ttu-id="349d4-373">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="349d4-373">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="349d4-374">使用 Azure PowerShell 管理 HDInsight</span><span class="sxs-lookup"><span data-stu-id="349d4-374">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="349d4-375">使用 Azure CLI 管理 HDInsight</span><span class="sxs-lookup"><span data-stu-id="349d4-375">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="349d4-376">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="349d4-376">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="349d4-377">在 HDInsight 中使用 Hive</span><span class="sxs-lookup"><span data-stu-id="349d4-377">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="349d4-378">在 HDInsight 中使用 Pig</span><span class="sxs-lookup"><span data-stu-id="349d4-378">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="349d4-379">在 HDInsight 中使用 Sqoop</span><span class="sxs-lookup"><span data-stu-id="349d4-379">Use Sqoop in HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="349d4-380">開始使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="349d4-380">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="349d4-381">Azure HDInsight 提供 Hadoop 的什麼版本？</span><span class="sxs-lookup"><span data-stu-id="349d4-381">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop 命令列"
