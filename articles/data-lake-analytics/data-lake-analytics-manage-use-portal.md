---
title: "使用的 Azure Data Lake Analytics aaaManage hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 toomanage Data Lake Analytics 帳戶的必要項，資料來源、 使用者和工作。"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="11a6f-103">使用 hello Azure 入口網站來管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="11a6f-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="11a6f-104">了解 toomanage Azure Data Lake Analytics 帳戶、 帳戶資料來源、 使用者和工作使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="11a6f-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="11a6f-105">toosee 管理主題，需使用其他工具中，按一下 在 hello hello 頁面最上方的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="11a6f-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="11a6f-106">管理 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="11a6f-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="11a6f-107">建立帳戶</span><span class="sxs-lookup"><span data-stu-id="11a6f-107">Create an account</span></span>

1. <span data-ttu-id="11a6f-108">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="11a6f-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="11a6f-109">按一下 [新增] > [智慧 + 分析] > [Data Lake Analytics]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="11a6f-110">選取下列項目 hello 的值：</span><span class="sxs-lookup"><span data-stu-id="11a6f-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="11a6f-111">**名稱**: hello hello Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="11a6f-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="11a6f-112">**訂用帳戶**: hello hello 帳戶所使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="11a6f-113">**資源群組**: hello Azure 資源群組中哪個 toocreate hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="11a6f-114">**位置**: hello hello Data Lake Analytics 帳戶的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="11a6f-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="11a6f-115">**Data Lake Store**: hello hello Data Lake Analytics 帳戶所使用的預設存放區 toobe。</span><span class="sxs-lookup"><span data-stu-id="11a6f-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="11a6f-116">hello Azure Data Lake Store 帳戶和 hello 資料湖分析帳戶必須在 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="11a6f-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="11a6f-117">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="11a6f-118">刪除 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="11a6f-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="11a6f-119">在您刪除 Data Lake Analytics 帳戶前，請先刪除其預設 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="11a6f-120">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-121">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-121">Click **Delete**.</span></span>
3. <span data-ttu-id="11a6f-122">型別 hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="11a6f-122">Type hello account name.</span></span>
4. <span data-ttu-id="11a6f-123">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="11a6f-124">管理資料來源</span><span class="sxs-lookup"><span data-stu-id="11a6f-124">Manage data sources</span></span>

<span data-ttu-id="11a6f-125">Data Lake Analytics 支援下列資料來源的 hello:</span><span class="sxs-lookup"><span data-stu-id="11a6f-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="11a6f-126">資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="11a6f-126">Data Lake Store</span></span>
* <span data-ttu-id="11a6f-127">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="11a6f-127">Azure Storage</span></span>

<span data-ttu-id="11a6f-128">您可以使用資料總管 toobrowse 資料來源，以及執行基本的檔案管理作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="11a6f-129">建立資料來源</span><span class="sxs-lookup"><span data-stu-id="11a6f-129">Add a data source</span></span>

1. <span data-ttu-id="11a6f-130">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-131">按一下 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="11a6f-132">按一下 [ **新增資料來源**]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="11a6f-133">tooadd Data Lake Store 帳戶，您需要 hello 帳戶名稱和存取 toohello 帳戶 toobe 無法 tooquery 它。</span><span class="sxs-lookup"><span data-stu-id="11a6f-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="11a6f-134">tooadd Azure Blob 儲存體，您需要 hello 儲存體帳戶和 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="11a6f-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="11a6f-135">toofind 它們，請移 toohello hello 入口網站中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="11a6f-136">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="11a6f-136">Set up firewall rules</span></span>

<span data-ttu-id="11a6f-137">您可以使用 Data Lake Analytics toofurther 鎖定存取 tooyour Data Lake Analytics 帳戶在 hello 網路層級。</span><span class="sxs-lookup"><span data-stu-id="11a6f-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="11a6f-138">您可以啟用防火牆、指定 IP 位址或為受信任的用戶端定義 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="11a6f-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="11a6f-139">啟用這些量值之後，只有具有 hello hello 定義範圍內的 IP 位址的用戶端可以連接到 toohello 存放區。</span><span class="sxs-lookup"><span data-stu-id="11a6f-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="11a6f-140">如果其他 Azure 服務，例如 Azure Data Factory 或 Vm，toohello Data Lake Analytics 帳戶的連接，請確定**允許 Azure 服務**開啟**上**。</span><span class="sxs-lookup"><span data-stu-id="11a6f-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="11a6f-141">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="11a6f-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="11a6f-142">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-143">在左側 hello hello 功能表上，按一下**防火牆**。</span><span class="sxs-lookup"><span data-stu-id="11a6f-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="11a6f-144">新增使用者</span><span class="sxs-lookup"><span data-stu-id="11a6f-144">Add a new user</span></span>

<span data-ttu-id="11a6f-145">您可以使用 hello**新增使用者精靈**tooeasily 新的資料湖使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="11a6f-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="11a6f-146">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-147">在 hello 左、 下**入門**，按一下 **新增使用者精靈**。</span><span class="sxs-lookup"><span data-stu-id="11a6f-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="11a6f-148">選取使用者，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="11a6f-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="11a6f-149">選取角色，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="11a6f-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="11a6f-150">設定新的開發人員 toouse Azure 資料湖選取 hello tooset**資料湖分析開發人員**角色。</span><span class="sxs-lookup"><span data-stu-id="11a6f-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="11a6f-151">選取 hello 存取控制清單 (Acl) 的 hello U SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="11a6f-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="11a6f-152">當您對您的選擇感到滿意時，請按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="11a6f-153">選取檔案的 hello Acl。</span><span class="sxs-lookup"><span data-stu-id="11a6f-153">Select hello ACLs for files.</span></span> <span data-ttu-id="11a6f-154">對於 hello 預設存放區，請不要變更 hello 根資料夾的 hello Acl"/"和 hello/系統資料夾。</span><span class="sxs-lookup"><span data-stu-id="11a6f-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="11a6f-155">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-155">Click **Select**.</span></span>
7. <span data-ttu-id="11a6f-156">檢閱您選取的所有變更，然後按一下執行。</span><span class="sxs-lookup"><span data-stu-id="11a6f-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="11a6f-157">Hello 精靈完成時，請按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="11a6f-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="11a6f-158">管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="11a6f-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="11a6f-159">如同其他 Azure 服務，您可以使用角色型存取控制 (RBAC) toocontrol 使用者互動的方式與 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="11a6f-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="11a6f-160">hello 標準 RBAC 角色有下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="11a6f-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="11a6f-161">**擁有者**： 可以將工作提交、 監控工作、 取消工作，從任何使用者，並設定 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="11a6f-162">**參與者**： 可以將工作提交、 監控工作、 取消工作，從任何使用者，並設定 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="11a6f-163">**讀取者**：可以監視作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="11a6f-164">使用 hello 資料湖分析開發人員角色 tooenable U-SQL 開發人員 toouse hello 資料湖分析服務。</span><span class="sxs-lookup"><span data-stu-id="11a6f-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="11a6f-165">您可以使用 hello 資料湖分析開發人員角色：</span><span class="sxs-lookup"><span data-stu-id="11a6f-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="11a6f-166">提交作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-166">Submit jobs.</span></span>
* <span data-ttu-id="11a6f-167">監視工作狀態和 hello 任何的進度使用者所提交的工作。</span><span class="sxs-lookup"><span data-stu-id="11a6f-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="11a6f-168">請參閱 hello U-SQL 指令碼，從任何使用者所提交的作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="11a6f-169">只取消您自己的作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="11a6f-170">新增使用者或安全性群組 tooa Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="11a6f-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="11a6f-171">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-172">按一下 [存取控制 (IAM)] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="11a6f-173">選取角色。</span><span class="sxs-lookup"><span data-stu-id="11a6f-173">Select a role.</span></span>
4. <span data-ttu-id="11a6f-174">新增使用者。</span><span class="sxs-lookup"><span data-stu-id="11a6f-174">Add a user.</span></span>
5. <span data-ttu-id="11a6f-175">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="11a6f-176">如果使用者或安全性群組需要 toosubmit 工作，他們也需要 hello 存放區帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="11a6f-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="11a6f-177">如需詳細資訊，請參閱[保護儲存在 Data Lake Store 中的資料](../data-lake-store/data-lake-store-secure-data.md)。</span><span class="sxs-lookup"><span data-stu-id="11a6f-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="11a6f-178">管理工作</span><span class="sxs-lookup"><span data-stu-id="11a6f-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="11a6f-179">提交作業</span><span class="sxs-lookup"><span data-stu-id="11a6f-179">Submit a job</span></span>

1. <span data-ttu-id="11a6f-180">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="11a6f-181">按一下 [ **新增工作**]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-181">Click **New Job**.</span></span> <span data-ttu-id="11a6f-182">對於每項作業，請設定：</span><span class="sxs-lookup"><span data-stu-id="11a6f-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="11a6f-183">**工作名稱**: hello hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="11a6f-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="11a6f-184">**優先順序**：數字越小，優先順序越高。</span><span class="sxs-lookup"><span data-stu-id="11a6f-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="11a6f-185">如果兩個工作會排入佇列，值較低優先順序的 hello 其中一個會執行第一次。</span><span class="sxs-lookup"><span data-stu-id="11a6f-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="11a6f-186">**平行處理原則**: hello 最大數目計算處理 tooreserve 此作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="11a6f-187">按一下 [ **提交作業**]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="11a6f-188">監視工作</span><span class="sxs-lookup"><span data-stu-id="11a6f-188">Monitor jobs</span></span>

1. <span data-ttu-id="11a6f-189">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-190">按一下 [檢視所有作業]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-190">Click **View All Jobs**.</span></span> <span data-ttu-id="11a6f-191">顯示所有 hello 帳戶中的 hello 作用中和最近完成工作的清單。</span><span class="sxs-lookup"><span data-stu-id="11a6f-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="11a6f-192">（選擇性） 按一下**篩選**toohelp 尋找 hello 工作依**時間範圍**，**工作名稱**，和**作者**值。</span><span class="sxs-lookup"><span data-stu-id="11a6f-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="11a6f-193">監視管線作業</span><span class="sxs-lookup"><span data-stu-id="11a6f-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="11a6f-194">屬於管線的作業工作分組，通常就循序 tooaccomplish 特定案例。</span><span class="sxs-lookup"><span data-stu-id="11a6f-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="11a6f-195">例如，您可以有一個管線，來清除、擷取、轉換、彙總客戶深入解析的使用。</span><span class="sxs-lookup"><span data-stu-id="11a6f-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="11a6f-196">識別管線工作提交 hello 作業時，使用 hello 「 管線 」 屬性。</span><span class="sxs-lookup"><span data-stu-id="11a6f-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="11a6f-197">使用 ADF V2 排程的作業會自動填入此屬性。</span><span class="sxs-lookup"><span data-stu-id="11a6f-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="11a6f-198">tooview U-SQL 工作屬於管線的清單：</span><span class="sxs-lookup"><span data-stu-id="11a6f-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="11a6f-199">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="11a6f-200">按一下 [作業深入解析]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-200">Click **Job Insights**.</span></span> <span data-ttu-id="11a6f-201">[所有工作] 索引標籤將預設，顯示一份執行中、 hello 排入佇列，並結束作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="11a6f-202">按一下 hello**管線作業** 索引標籤。這會顯示管線作業清單，以及每個管線的彙總統計資料。</span><span class="sxs-lookup"><span data-stu-id="11a6f-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="11a6f-203">監視週期性作業</span><span class="sxs-lookup"><span data-stu-id="11a6f-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="11a6f-204">重複執行的作業是指具有 hello 相同的商務邏輯但使用不同的輸入的資料，它一次。</span><span class="sxs-lookup"><span data-stu-id="11a6f-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="11a6f-205">在理想情況下，一定會成功，並有相當穩定的執行時間; 週期性工作監視這些行為有助於確定 hello 作業為狀況良好。</span><span class="sxs-lookup"><span data-stu-id="11a6f-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="11a6f-206">週期性工作，會識別使用 hello"Recurrence"屬性。</span><span class="sxs-lookup"><span data-stu-id="11a6f-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="11a6f-207">使用 ADF V2 排程的作業會自動填入此屬性。</span><span class="sxs-lookup"><span data-stu-id="11a6f-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="11a6f-208">tooview 週期性的 U-SQL 工作清單：</span><span class="sxs-lookup"><span data-stu-id="11a6f-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="11a6f-209">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="11a6f-210">按一下 [作業深入解析]。</span><span class="sxs-lookup"><span data-stu-id="11a6f-210">Click **Job Insights**.</span></span> <span data-ttu-id="11a6f-211">[所有工作] 索引標籤將預設，顯示一份執行中、 hello 排入佇列，並結束作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="11a6f-212">按一下 hello**週期性工作** 索引標籤。這會顯示週期性作業清單，以及每個週期性作業的彙總統計資料。</span><span class="sxs-lookup"><span data-stu-id="11a6f-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="11a6f-213">管理原則</span><span class="sxs-lookup"><span data-stu-id="11a6f-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="11a6f-214">帳戶層級原則</span><span class="sxs-lookup"><span data-stu-id="11a6f-214">Account-level policies</span></span>

<span data-ttu-id="11a6f-215">這些原則會套用 tooall Data Lake Analytics 帳戶中的工作。</span><span class="sxs-lookup"><span data-stu-id="11a6f-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="11a6f-216">Data Lake Analytics 帳戶中的 AU 數目上限</span><span class="sxs-lookup"><span data-stu-id="11a6f-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="11a6f-217">原則會控制 hello 分析單位總數 (AUs) 可以使用 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="11a6f-218">根據預設，設定 too250 hello 值。</span><span class="sxs-lookup"><span data-stu-id="11a6f-218">By default, hello value is set too250.</span></span> <span data-ttu-id="11a6f-219">比方說，如果此值設定 too250 澳洲，您可以有 250 澳洲指派 tooit，以執行的一項作業或 10 個工作執行與 25 澳洲每個。</span><span class="sxs-lookup"><span data-stu-id="11a6f-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="11a6f-220">送出的其他工作會排入佇列，直到 hello 正在執行的作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="11a6f-221">澳洲正在執行的作業完成時，會釋放給 hello toorun 工作排入佇列。</span><span class="sxs-lookup"><span data-stu-id="11a6f-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="11a6f-222">toochange hello 數目澳洲 Data Lake Analytics 帳戶：</span><span class="sxs-lookup"><span data-stu-id="11a6f-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="11a6f-223">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-224">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-224">Click **Properties**.</span></span>
3. <span data-ttu-id="11a6f-225">在下**最大澳洲**、 移動 hello 滑桿 tooselect 值，或在 hello 文字方塊中輸入 hello 值。</span><span class="sxs-lookup"><span data-stu-id="11a6f-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="11a6f-226">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="11a6f-227">如果您需要多個 hello 預設 （250 個） 澳洲，在 hello 入口網站中，按一下 **說明 + 支援**toosubmit 支援要求。</span><span class="sxs-lookup"><span data-stu-id="11a6f-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="11a6f-228">可以增加 hello 澳洲 Data Lake Analytics 帳戶中所提供的數目。</span><span class="sxs-lookup"><span data-stu-id="11a6f-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="11a6f-229">可以同時執行的作業數目上限</span><span class="sxs-lookup"><span data-stu-id="11a6f-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="11a6f-230">原則會控制多少的工作都可以在 hello 執行相同的時間。</span><span class="sxs-lookup"><span data-stu-id="11a6f-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="11a6f-231">根據預設，這個值會設定 too20。</span><span class="sxs-lookup"><span data-stu-id="11a6f-231">By default, this value is set too20.</span></span> <span data-ttu-id="11a6f-232">如果您的 Data Lake Analytics 澳洲可用，新的工作，才排程的 toorun 立即 hello 執行工作的總數目達到 hello 值，這個原則。</span><span class="sxs-lookup"><span data-stu-id="11a6f-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="11a6f-233">當您到達 hello 可以同時執行的作業數目上限時，後續的工作會依優先順序佇列，直到一或多個執行中的工作完成 （取決於 AU 可用性）。</span><span class="sxs-lookup"><span data-stu-id="11a6f-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="11a6f-234">toochange hello 數目可以同時執行的作業：</span><span class="sxs-lookup"><span data-stu-id="11a6f-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="11a6f-235">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-236">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-236">Click **Properties**.</span></span>
3. <span data-ttu-id="11a6f-237">在下**最大數目的執行工作**、 移動 hello 滑桿 tooselect 值，或在 hello 文字方塊中輸入 hello 值。</span><span class="sxs-lookup"><span data-stu-id="11a6f-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="11a6f-238">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="11a6f-239">如果您需要更多超過 hello 預設 (20) 中的工作數目，hello 入口網站中，按一下的 toorun**說明 + 支援**toosubmit 支援要求。</span><span class="sxs-lookup"><span data-stu-id="11a6f-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="11a6f-240">可以增加 hello Data Lake Analytics 帳戶中可以同時執行的作業數目。</span><span class="sxs-lookup"><span data-stu-id="11a6f-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="11a6f-241">多久 tookeep 工作中繼資料和資源</span><span class="sxs-lookup"><span data-stu-id="11a6f-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="11a6f-242">當您的使用者執行 U SQL 作業時，hello 資料湖分析服務會保留所有相關的檔案。</span><span class="sxs-lookup"><span data-stu-id="11a6f-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="11a6f-243">相關的檔案包含 hello U-SQL 指令碼，hello hello U-SQL 指令碼、 已編譯的資源，與統計資料中參考的 DLL 檔案。</span><span class="sxs-lookup"><span data-stu-id="11a6f-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="11a6f-244">hello 檔案位於 hello /system/ 資料夾中的 hello 預設 Azure 資料湖存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="11a6f-245">此原則會控制會自動刪除之前要儲存這些資源的時間長度 （hello 預設為 30 天）。</span><span class="sxs-lookup"><span data-stu-id="11a6f-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="11a6f-246">偵錯，以及您將在未來的 hello 重新執行的工作的效能微調，您可以使用這些檔案。</span><span class="sxs-lookup"><span data-stu-id="11a6f-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="11a6f-247">toochange 多久 tookeep 工作中繼資料和資源：</span><span class="sxs-lookup"><span data-stu-id="11a6f-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="11a6f-248">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-249">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-249">Click **Properties**.</span></span>
3. <span data-ttu-id="11a6f-250">在下**天 tooRetain 工作查詢**、 移動 hello 滑桿 tooselect 值，或在 hello 文字方塊中輸入 hello 值。</span><span class="sxs-lookup"><span data-stu-id="11a6f-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="11a6f-251">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="11a6f-252">作業層級原則</span><span class="sxs-lookup"><span data-stu-id="11a6f-252">Job-level policies</span></span>
<span data-ttu-id="11a6f-253">您可以使用工作層級原則，控制 hello 最大澳洲和 hello 個別的使用者 （或特定安全性群組的成員） 可以在他們所提交的工作設定的最高優先順序。</span><span class="sxs-lookup"><span data-stu-id="11a6f-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="11a6f-254">這可讓您控制使用者所造成的 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="11a6f-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="11a6f-255">它也可讓您控制的排程工作的 hello 效果可能會有高優先權上正在執行中的實際執行工作 hello 相同的資料湖分析帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="11a6f-256">資料湖分析有兩個您可以在 hello 作業層級設定的原則：</span><span class="sxs-lookup"><span data-stu-id="11a6f-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="11a6f-257">**AU 限制每個作業**： 使用者只能提交 toothis 數目澳洲正常的作業。</span><span class="sxs-lookup"><span data-stu-id="11a6f-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="11a6f-258">根據預設，這項限制是 hello 與 hello AU 上限 hello 帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="11a6f-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="11a6f-259">**優先順序**： 使用者只能提交工作的優先權低於或等於 toothis 值。</span><span class="sxs-lookup"><span data-stu-id="11a6f-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="11a6f-260">請注意，數字較高表示優先順序較低。</span><span class="sxs-lookup"><span data-stu-id="11a6f-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="11a6f-261">根據預設，這會設定 too1，這是 hello 高的可能優先權。</span><span class="sxs-lookup"><span data-stu-id="11a6f-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="11a6f-262">每個帳戶都已設定預設原則。</span><span class="sxs-lookup"><span data-stu-id="11a6f-262">There is a default policy set on every account.</span></span> <span data-ttu-id="11a6f-263">hello 預設原則適用於 tooall 的 hello 帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="11a6f-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="11a6f-264">您可以針對特定使用者和群組設定其他原則。</span><span class="sxs-lookup"><span data-stu-id="11a6f-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="11a6f-265">帳戶層級原則和作業層級原則可同時套用。</span><span class="sxs-lookup"><span data-stu-id="11a6f-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="11a6f-266">新增特定使用者或群組的原則</span><span class="sxs-lookup"><span data-stu-id="11a6f-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="11a6f-267">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-268">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-268">Click **Properties**.</span></span>
3. <span data-ttu-id="11a6f-269">在下**工作提交限制**，按一下 hello**新增原則** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11a6f-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="11a6f-270">然後，選取或輸入 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="11a6f-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="11a6f-271">**計算原則名稱**： 輸入原則名稱，tooremind 您 hello 目的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="11a6f-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="11a6f-272">**選取使用者或群組**: hello 使用者或群組，此原則適用於選取。</span><span class="sxs-lookup"><span data-stu-id="11a6f-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="11a6f-273">**設定工作 AU 限制 hello**: hello AU 限制適用於 toohello 選取使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="11a6f-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="11a6f-274">**設定優先順序限制 hello**: hello 優先順序限制適用於 toohello 選取使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="11a6f-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="11a6f-275">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-275">Click **Ok**.</span></span>

5. <span data-ttu-id="11a6f-276">hello 新原則會列在 hello**預設**底下原則資料表**工作提交限制**。</span><span class="sxs-lookup"><span data-stu-id="11a6f-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="11a6f-277">刪除或編輯現有原則</span><span class="sxs-lookup"><span data-stu-id="11a6f-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="11a6f-278">在 hello Azure 入口網站，移 tooyour Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11a6f-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="11a6f-279">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="11a6f-279">Click **Properties**.</span></span>
3. <span data-ttu-id="11a6f-280">在下**工作提交限制**，尋找您想 tooedit 的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="11a6f-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="11a6f-281">toosee hello**刪除**和**編輯**hello hello 資料表的最右邊資料行中的選項，請按一下**...**.</span><span class="sxs-lookup"><span data-stu-id="11a6f-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="11a6f-282">作業原則的其他資源</span><span class="sxs-lookup"><span data-stu-id="11a6f-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="11a6f-283">原則概觀部落格文章</span><span class="sxs-lookup"><span data-stu-id="11a6f-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="11a6f-284">帳戶層級原則部落格文章</span><span class="sxs-lookup"><span data-stu-id="11a6f-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="11a6f-285">作業層級原則部落格文章</span><span class="sxs-lookup"><span data-stu-id="11a6f-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="11a6f-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11a6f-286">Next steps</span></span>

* [<span data-ttu-id="11a6f-287">Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="11a6f-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="11a6f-288">開始使用 Data Lake Analytics 使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="11a6f-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="11a6f-289">使用 Azure PowerShell 管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="11a6f-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

