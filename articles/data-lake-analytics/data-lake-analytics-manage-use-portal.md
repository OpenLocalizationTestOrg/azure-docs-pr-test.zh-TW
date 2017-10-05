---
title: "使用 Azure 入口網站管理 Azure Data Lake Analytics | Microsoft Docs"
description: "瞭解如何管理 Data Lake Analytics 帳戶、資料來源、使用者和作業。"
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
ms.openlocfilehash: e49d1a0e0ccc6567d0a6841817667717ff5dba76
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-the-azure-portal"></a><span data-ttu-id="57f13-103">使用 Azure 入口網站管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="57f13-103">Manage Azure Data Lake Analytics by using the Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="57f13-104">了解如何使用 Azure 入口網站來管理 Azure Data Lake Analytics 帳戶、帳戶資料來源、使用者及作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-104">Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using the Azure portal.</span></span> <span data-ttu-id="57f13-105">若要查看有關使用其他工具的管理主題，請按一下頁面頂端的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="57f13-105">To see management topics about using other tools, click a tab at the top of the page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="57f13-106">管理 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="57f13-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="57f13-107">建立帳戶</span><span class="sxs-lookup"><span data-stu-id="57f13-107">Create an account</span></span>

1. <span data-ttu-id="57f13-108">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="57f13-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="57f13-109">按一下 [新增] > [智慧 + 分析] > [Data Lake Analytics]。</span><span class="sxs-lookup"><span data-stu-id="57f13-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="57f13-110">選取下列項目的值︰</span><span class="sxs-lookup"><span data-stu-id="57f13-110">Select values for the following items:</span></span> 
   1. <span data-ttu-id="57f13-111">**名稱**：Data Lake Analytics 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="57f13-111">**Name**: The name of the Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="57f13-112">**訂用帳戶**：用於此帳戶的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-112">**Subscription**: The Azure subscription used for the account.</span></span>
   3. <span data-ttu-id="57f13-113">**資源群組**：在其中建立帳戶的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="57f13-113">**Resource Group**: The Azure resource group in which to create the account.</span></span> 
   4. <span data-ttu-id="57f13-114">**位置**：Data Lake Analytics 帳戶的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="57f13-114">**Location**: The Azure datacenter for the Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="57f13-115">**Data Lake Store**：Data Lake Analytics 帳戶所要使用的預設存放區。</span><span class="sxs-lookup"><span data-stu-id="57f13-115">**Data Lake Store**: The default store to be used for the Data Lake Analytics account.</span></span> <span data-ttu-id="57f13-116">Azure Data Lake Store 帳戶和 Data Lake Analytics 帳戶必須位於相同位置。</span><span class="sxs-lookup"><span data-stu-id="57f13-116">The Azure Data Lake Store account and the Data Lake Analytics account must be in the same location.</span></span>
4. <span data-ttu-id="57f13-117">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="57f13-118">刪除 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="57f13-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="57f13-119">在您刪除 Data Lake Analytics 帳戶前，請先刪除其預設 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="57f13-120">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-120">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-121">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-121">Click **Delete**.</span></span>
3. <span data-ttu-id="57f13-122">輸入帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="57f13-122">Type the account name.</span></span>
4. <span data-ttu-id="57f13-123">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="57f13-124">管理資料來源</span><span class="sxs-lookup"><span data-stu-id="57f13-124">Manage data sources</span></span>

<span data-ttu-id="57f13-125">Data Lake Analytics 支援下列資料來源：</span><span class="sxs-lookup"><span data-stu-id="57f13-125">Data Lake Analytics supports the following data sources:</span></span>

* <span data-ttu-id="57f13-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="57f13-126">Data Lake Store</span></span>
* <span data-ttu-id="57f13-127">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="57f13-127">Azure Storage</span></span>

<span data-ttu-id="57f13-128">您可以使用 [資料總管] 來瀏覽資料來源和執行基本檔案管理作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-128">You can use Data Explorer to browse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="57f13-129">建立資料來源</span><span class="sxs-lookup"><span data-stu-id="57f13-129">Add a data source</span></span>

1. <span data-ttu-id="57f13-130">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-130">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-131">按一下 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="57f13-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="57f13-132">按一下 [ **新增資料來源**]。</span><span class="sxs-lookup"><span data-stu-id="57f13-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="57f13-133">若要新增 Azure Data Lake Store 帳戶，您需要帳戶名稱及帳戶的存取權才可進行查詢。</span><span class="sxs-lookup"><span data-stu-id="57f13-133">To add a Data Lake Store account, you need the account name and access to the account to be able to query it.</span></span>
   * <span data-ttu-id="57f13-134">若要新增 Azure Blob 儲存體，您需要儲存體帳戶和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="57f13-134">To add Azure Blob storage, you need the storage account and the account key.</span></span> <span data-ttu-id="57f13-135">若要找到它們，請在入口網站中移至此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-135">To find them, go to the storage account in the portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="57f13-136">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="57f13-136">Set up firewall rules</span></span>

<span data-ttu-id="57f13-137">您可以使用 Data Lake Analytics，進一步在網路層級鎖定 Data Lake Analytics 帳戶的存取。</span><span class="sxs-lookup"><span data-stu-id="57f13-137">You can use Data Lake Analytics to further lock down access to your Data Lake Analytics account at the network level.</span></span> <span data-ttu-id="57f13-138">您可以啟用防火牆、指定 IP 位址或為受信任的用戶端定義 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="57f13-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="57f13-139">啟用這些量值之後，只有具有定義範圍內 IP 位址的用戶端可以連線到存放區。</span><span class="sxs-lookup"><span data-stu-id="57f13-139">After you enable these measures, only clients that have the IP addresses within the defined range can connect to the store.</span></span>

<span data-ttu-id="57f13-140">如果有其他 Azure 服務 (例如 Azure Data Factory 或 VM) 連線到 Data Lake Analytics 帳戶，請確定 [允許 Azure 服務] 已 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="57f13-140">If other Azure services, like Azure Data Factory or VMs, connect to the Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="57f13-141">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="57f13-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="57f13-142">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-142">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-143">在左側功能表上，按一下 [防火牆]。</span><span class="sxs-lookup"><span data-stu-id="57f13-143">On the menu on the left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="57f13-144">新增使用者</span><span class="sxs-lookup"><span data-stu-id="57f13-144">Add a new user</span></span>

<span data-ttu-id="57f13-145">您可以使用 [新增使用者精靈] 輕鬆地佈建新的 Data Lake 使用者。</span><span class="sxs-lookup"><span data-stu-id="57f13-145">You can use the **Add User Wizard** to easily provision new Data Lake users.</span></span>

1. <span data-ttu-id="57f13-146">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-146">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-147">在左側 [快速入門] 之下，按一下 [新增使用者精靈]。</span><span class="sxs-lookup"><span data-stu-id="57f13-147">On the left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="57f13-148">選取使用者，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="57f13-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="57f13-149">選取角色，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="57f13-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="57f13-150">若要設定新的開發人員以使用 Azure Data Lake，請選取 [Data Lake Analytics 開發人員] 角色。</span><span class="sxs-lookup"><span data-stu-id="57f13-150">To set up a new developer to use Azure Data Lake, select the **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="57f13-151">選取 U-SQL 資料庫的存取控制清單 (ACL)。</span><span class="sxs-lookup"><span data-stu-id="57f13-151">Select the access control lists (ACLs) for the U-SQL databases.</span></span> <span data-ttu-id="57f13-152">當您對您的選擇感到滿意時，請按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="57f13-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="57f13-153">選取檔案的 ACL。</span><span class="sxs-lookup"><span data-stu-id="57f13-153">Select the ACLs for files.</span></span> <span data-ttu-id="57f13-154">對於預設存放區，請不要變更根資料夾 "/" 和 /system 資料夾的 ACL。</span><span class="sxs-lookup"><span data-stu-id="57f13-154">For the default store, don't change the ACLs for the root folder "/" and for the /system folder.</span></span> <span data-ttu-id="57f13-155">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-155">Click **Select**.</span></span>
7. <span data-ttu-id="57f13-156">檢閱您選取的所有變更，然後按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="57f13-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="57f13-157">當精靈完成時，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="57f13-157">When the wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="57f13-158">管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="57f13-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="57f13-159">如同其他 Azure 服務，您可以使用角色型存取控制 (RBAC) 來控制使用者與服務互動的方式。</span><span class="sxs-lookup"><span data-stu-id="57f13-159">Like other Azure services, you can use Role-Based Access Control (RBAC) to control how users interact with the service.</span></span>

<span data-ttu-id="57f13-160">標準 RBAC 角色具有下列功能：</span><span class="sxs-lookup"><span data-stu-id="57f13-160">The standard RBAC roles have the following capabilities:</span></span>
* <span data-ttu-id="57f13-161">**擁有者**：可以提交、監視、取消任何使用者的作業，以及設定帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="57f13-162">**參與者**：可以提交、監視、取消任何使用者的作業，以及設定帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="57f13-163">**讀取者**：可以監視作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="57f13-164">使用 Data Lake Analytics 開發人員角色來啟用 U-SQL 開發人員，以使用 Data Lake Analytics 服務。</span><span class="sxs-lookup"><span data-stu-id="57f13-164">Use the Data Lake Analytics Developer role to enable U-SQL developers to use the Data Lake Analytics service.</span></span> <span data-ttu-id="57f13-165">您可以使用 Data Lake Analytics 開發人員角色來：</span><span class="sxs-lookup"><span data-stu-id="57f13-165">You can use the Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="57f13-166">提交作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-166">Submit jobs.</span></span>
* <span data-ttu-id="57f13-167">監視任何使用者所提交作業的作業狀態和進度。</span><span class="sxs-lookup"><span data-stu-id="57f13-167">Monitor job status and the progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="57f13-168">請參閱任何使用者所提交作業中的 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="57f13-168">See the U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="57f13-169">只取消您自己的作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-to-a-data-lake-analytics-account"></a><span data-ttu-id="57f13-170">將使用者或安全性群組新增到 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="57f13-170">Add users or security groups to a Data Lake Analytics account</span></span>

1. <span data-ttu-id="57f13-171">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-171">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-172">按一下 [存取控制 (IAM)] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="57f13-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="57f13-173">選取角色。</span><span class="sxs-lookup"><span data-stu-id="57f13-173">Select a role.</span></span>
4. <span data-ttu-id="57f13-174">新增使用者。</span><span class="sxs-lookup"><span data-stu-id="57f13-174">Add a user.</span></span>
5. <span data-ttu-id="57f13-175">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="57f13-176">如果使用者或安全性群組需要提交作業，他們也需要有存放區帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="57f13-176">If a user or a security group needs to submit jobs, they also need permission on the store account.</span></span> <span data-ttu-id="57f13-177">如需詳細資訊，請參閱[保護儲存在 Data Lake Store 中的資料](../data-lake-store/data-lake-store-secure-data.md)。</span><span class="sxs-lookup"><span data-stu-id="57f13-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="57f13-178">管理工作</span><span class="sxs-lookup"><span data-stu-id="57f13-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="57f13-179">提交作業</span><span class="sxs-lookup"><span data-stu-id="57f13-179">Submit a job</span></span>

1. <span data-ttu-id="57f13-180">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-180">In the Azure portal, go to your Data Lake Analytics account.</span></span>

2. <span data-ttu-id="57f13-181">按一下 [ **新增工作**]。</span><span class="sxs-lookup"><span data-stu-id="57f13-181">Click **New Job**.</span></span> <span data-ttu-id="57f13-182">對於每項作業，請設定：</span><span class="sxs-lookup"><span data-stu-id="57f13-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="57f13-183">**作業名稱**：作業名稱。</span><span class="sxs-lookup"><span data-stu-id="57f13-183">**Job Name**: The name of the job.</span></span>
    2. <span data-ttu-id="57f13-184">**優先順序**：數字越小，優先順序越高。</span><span class="sxs-lookup"><span data-stu-id="57f13-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="57f13-185">如果有兩項作業排入佇列，優先順序值較小的作業會優先執行。</span><span class="sxs-lookup"><span data-stu-id="57f13-185">If two jobs are queued, the one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="57f13-186">**平行處理原則**：要為此作業保留的計算程序數目上限。</span><span class="sxs-lookup"><span data-stu-id="57f13-186">**Parallelism**: The maximum number of compute processes to reserve for this job.</span></span>

3. <span data-ttu-id="57f13-187">按一下 [ **提交作業**]。</span><span class="sxs-lookup"><span data-stu-id="57f13-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="57f13-188">監視工作</span><span class="sxs-lookup"><span data-stu-id="57f13-188">Monitor jobs</span></span>

1. <span data-ttu-id="57f13-189">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-189">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-190">按一下 [檢視所有作業]。</span><span class="sxs-lookup"><span data-stu-id="57f13-190">Click **View All Jobs**.</span></span> <span data-ttu-id="57f13-191">隨即顯示帳戶中所有作用中和最近完成的作業清單。</span><span class="sxs-lookup"><span data-stu-id="57f13-191">A list of all the active and recently finished jobs in the account is shown.</span></span>
3. <span data-ttu-id="57f13-192">選擇性，按一下 [篩選] 可協助您依照 [時間範圍]、[作業名稱] 和 [作者] 值尋找作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-192">Optionally, click **Filter** to help you find the jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="57f13-193">監視管線作業</span><span class="sxs-lookup"><span data-stu-id="57f13-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="57f13-194">屬於某個管線的作業會搭配運作 (通常會循序進行)，以完成特定案例。</span><span class="sxs-lookup"><span data-stu-id="57f13-194">Jobs that are part of a pipeline work together, usually sequentially, to accomplish a specific scenario.</span></span> <span data-ttu-id="57f13-195">例如，您可以有一個管線，來清除、擷取、轉換、彙總客戶深入解析的使用。</span><span class="sxs-lookup"><span data-stu-id="57f13-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="57f13-196">提交作業之後，可使用 [管線] 屬性來找到管線作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-196">Pipeline jobs are identified using the "Pipeline" property when the job was submitted.</span></span> <span data-ttu-id="57f13-197">使用 ADF V2 排程的作業會自動填入此屬性。</span><span class="sxs-lookup"><span data-stu-id="57f13-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="57f13-198">若要檢視屬於管線的 U-SQL 作業清單：</span><span class="sxs-lookup"><span data-stu-id="57f13-198">To view a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="57f13-199">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-199">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="57f13-200">按一下 [作業深入解析]。</span><span class="sxs-lookup"><span data-stu-id="57f13-200">Click **Job Insights**.</span></span> <span data-ttu-id="57f13-201">預設會開啟 [所有作業] 索引標籤，其中顯示執行中、已佇列和已結束的作業清單。</span><span class="sxs-lookup"><span data-stu-id="57f13-201">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="57f13-202">按一下 [管線作業] 索引標籤。這會顯示管線作業清單，以及每個管線的彙總統計資料。</span><span class="sxs-lookup"><span data-stu-id="57f13-202">Click the **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="57f13-203">監視週期性作業</span><span class="sxs-lookup"><span data-stu-id="57f13-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="57f13-204">週期性作業是具有相同商務邏輯，但每次執行都會使用不同輸入資料的作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-204">A recurring job is one that has the same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="57f13-205">在理想情況下，週期性作業一律會成功，而且執行時間相當穩定；監視這些行為有助於確保作業狀況良好。</span><span class="sxs-lookup"><span data-stu-id="57f13-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure the job is healthy.</span></span> <span data-ttu-id="57f13-206">可使用 [週期性] 屬性來找到週期性作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-206">Recurring jobs are identified using the "Recurrence" property.</span></span> <span data-ttu-id="57f13-207">使用 ADF V2 排程的作業會自動填入此屬性。</span><span class="sxs-lookup"><span data-stu-id="57f13-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="57f13-208">若要檢視週期性的 U-SQL 作業清單：</span><span class="sxs-lookup"><span data-stu-id="57f13-208">To view a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="57f13-209">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-209">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="57f13-210">按一下 [作業深入解析]。</span><span class="sxs-lookup"><span data-stu-id="57f13-210">Click **Job Insights**.</span></span> <span data-ttu-id="57f13-211">預設會開啟 [所有作業] 索引標籤，其中顯示執行中、已佇列和已結束的作業清單。</span><span class="sxs-lookup"><span data-stu-id="57f13-211">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="57f13-212">按一下 [週期性作業] 索引標籤。這會顯示週期性作業清單，以及每個週期性作業的彙總統計資料。</span><span class="sxs-lookup"><span data-stu-id="57f13-212">Click the **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="57f13-213">管理原則</span><span class="sxs-lookup"><span data-stu-id="57f13-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="57f13-214">帳戶層級原則</span><span class="sxs-lookup"><span data-stu-id="57f13-214">Account-level policies</span></span>

<span data-ttu-id="57f13-215">這些原則會套用到 Data Lake Analytics 帳戶中的所有作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-215">These policies apply to all jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="57f13-216">Data Lake Analytics 帳戶中的 AU 數目上限</span><span class="sxs-lookup"><span data-stu-id="57f13-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="57f13-217">此原則控制 Data Lake Analytics 帳戶可以使用的分析單位 (AU) 總數。</span><span class="sxs-lookup"><span data-stu-id="57f13-217">A policy controls the total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="57f13-218">根據預設，此值設定為 250。</span><span class="sxs-lookup"><span data-stu-id="57f13-218">By default, the value is set to 250.</span></span> <span data-ttu-id="57f13-219">例如，如果此值設為 250 AU，您可以有一項已指派 250 AU 的執行中作業，或 10 項各有 25 AU 的執行中作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-219">For example, if this value is set to 250 AUs, you can have one job running with 250 AUs assigned to it, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="57f13-220">其他已提交的作業會排入佇列，直到執行中的作業完成為止。</span><span class="sxs-lookup"><span data-stu-id="57f13-220">Additional jobs that are submitted are queued until the running jobs are finished.</span></span> <span data-ttu-id="57f13-221">當執行中的作業完成時，會釋出 AU 以便執行已排入佇列的作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-221">When running jobs are finished, AUs are freed up for the queued jobs to run.</span></span>

<span data-ttu-id="57f13-222">若要變更 Data Lake Analytics 帳戶的 AU 數目：</span><span class="sxs-lookup"><span data-stu-id="57f13-222">To change the number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="57f13-223">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-223">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-224">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-224">Click **Properties**.</span></span>
3. <span data-ttu-id="57f13-225">在 [AU 上限] 之下，移動滑桿以選取值，或在文字方塊中輸入值。</span><span class="sxs-lookup"><span data-stu-id="57f13-225">Under **Maximum AUs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="57f13-226">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="57f13-227">如果您需要的 AU 超過預設值 (250)，請在入口網站中按一下 [說明 + 支援] 以提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="57f13-227">If you need more than the default (250) AUs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="57f13-228">您可以增加 Data Lake Analytics 帳戶中可用的 AU 數目。</span><span class="sxs-lookup"><span data-stu-id="57f13-228">The number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="57f13-229">可以同時執行的作業數目上限</span><span class="sxs-lookup"><span data-stu-id="57f13-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="57f13-230">此原則控制可以同時執行的多少作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-230">A policy controls how many jobs can run at the same time.</span></span> <span data-ttu-id="57f13-231">根據預設，此值設定為 20。</span><span class="sxs-lookup"><span data-stu-id="57f13-231">By default, this value is set to 20.</span></span> <span data-ttu-id="57f13-232">如果 Data Lake Analytics 有 AU 可用，則會安排立即執行新作業，直到執行中的作業總數達到此原則的值為止。</span><span class="sxs-lookup"><span data-stu-id="57f13-232">If your Data Lake Analytics has AUs available, new jobs are scheduled to run immediately until the total number of running jobs reaches the value of this policy.</span></span> <span data-ttu-id="57f13-233">當您達到可同時執行的作業數目上限時，後續作業會依優先順序排入佇列，直到一或多個執行中作業完成為止 (取決於 AU 可用性)。</span><span class="sxs-lookup"><span data-stu-id="57f13-233">When you reach the maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="57f13-234">若要變更可以同時執行的作業數目：</span><span class="sxs-lookup"><span data-stu-id="57f13-234">To change the number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="57f13-235">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-235">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-236">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-236">Click **Properties**.</span></span>
3. <span data-ttu-id="57f13-237">在 [執行中作業數目上限] 之下，移動滑桿以選取值，或在文字方塊中輸入值。</span><span class="sxs-lookup"><span data-stu-id="57f13-237">Under **Maximum Number of Running Jobs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="57f13-238">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="57f13-239">如果您需要執行的作業數目超過預設值 (20)，請在入口網站中按一下 [說明 + 支援] 以提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="57f13-239">If you need to run more than the default (20) number of jobs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="57f13-240">您可以增加 Data Lake Analytics 帳戶中可以同時執行的作業數目。</span><span class="sxs-lookup"><span data-stu-id="57f13-240">The number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-to-keep-job-metadata-and-resources"></a><span data-ttu-id="57f13-241">保留作業中繼資料和資源的時間長度</span><span class="sxs-lookup"><span data-stu-id="57f13-241">How long to keep job metadata and resources</span></span> 
<span data-ttu-id="57f13-242">當使用者執行 U-SQL 作業時，Data Lake Analytics 服務會保留所有相關的檔案。</span><span class="sxs-lookup"><span data-stu-id="57f13-242">When your users run U-SQL jobs, the Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="57f13-243">相關的檔案包括 U-SQL 指令碼、U-SQL 指令碼中參考的 DLL 檔案、已編譯的資源以及統計資料。</span><span class="sxs-lookup"><span data-stu-id="57f13-243">Related files include the U-SQL script, the DLL files referenced in the U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="57f13-244">這些檔案位於預設 Azure Data Lake 儲存體帳戶的 /system/ 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="57f13-244">The files are in the /system/ folder of the default Azure Data Lake Storage account.</span></span> <span data-ttu-id="57f13-245">此原則控制這些資源在自動刪除前的儲存時間長度 (預設值是 30 天)。</span><span class="sxs-lookup"><span data-stu-id="57f13-245">This policy controls how long these resources are stored before they are automatically deleted (the default is 30 days).</span></span> <span data-ttu-id="57f13-246">您可以使用這些檔案進行偵錯，以及未來將重新執行之作業的效能微調。</span><span class="sxs-lookup"><span data-stu-id="57f13-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in the future.</span></span>

<span data-ttu-id="57f13-247">若要變更保留作業中繼資料和資源的時間長度：</span><span class="sxs-lookup"><span data-stu-id="57f13-247">To change how long to keep job metadata and resources:</span></span>

1. <span data-ttu-id="57f13-248">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-248">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-249">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-249">Click **Properties**.</span></span>
3. <span data-ttu-id="57f13-250">在 [保留作業查詢的天數] 之下，移動滑桿以選取值，或在文字方塊中輸入值。</span><span class="sxs-lookup"><span data-stu-id="57f13-250">Under **Days to Retain Job Queries**, move the slider to select a value, or enter the value in the text box.</span></span>  
4. <span data-ttu-id="57f13-251">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="57f13-252">作業層級原則</span><span class="sxs-lookup"><span data-stu-id="57f13-252">Job-level policies</span></span>
<span data-ttu-id="57f13-253">使用工作層級原則，您可以控制 AU 上限和個別使用者 (或特定安全性群組的成員) 可以在其提交的作業上設定的最高優先順序。</span><span class="sxs-lookup"><span data-stu-id="57f13-253">With job-level policies, you can control the maximum AUs and the maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="57f13-254">這可讓您控制使用者所產生的成本。</span><span class="sxs-lookup"><span data-stu-id="57f13-254">This lets you control the costs incurred by users.</span></span> <span data-ttu-id="57f13-255">也可讓您控制已排程的作業可能對正在相同 Data Lake Analytics 帳戶中執行之高優先順序生產作業的影響。</span><span class="sxs-lookup"><span data-stu-id="57f13-255">It also lets you control the effect that scheduled jobs might have on high-priority production jobs that are running in the same Data Lake Analytics account.</span></span>

<span data-ttu-id="57f13-256">您可以在作業層級設定兩個 Data Lake Analytics 原則：</span><span class="sxs-lookup"><span data-stu-id="57f13-256">Data Lake Analytics has two policies that you can set at the job level:</span></span>

* <span data-ttu-id="57f13-257">**每個作業的 AU 限制**：使用者只能提交擁有的 AU 不超過此數目的作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-257">**AU limit per job**: Users can only submit jobs that have up to this number of AUs.</span></span> <span data-ttu-id="57f13-258">根據預設，此限制與帳戶的 AU 上限相同。</span><span class="sxs-lookup"><span data-stu-id="57f13-258">By default, this limit is the same as the maximum AU limit for the account.</span></span>
* <span data-ttu-id="57f13-259">**優先順序**：使用者只能提交優先順序低於或等於此值的作業。</span><span class="sxs-lookup"><span data-stu-id="57f13-259">**Priority**: Users can only submit jobs that have a priority lower than or equal to this value.</span></span> <span data-ttu-id="57f13-260">請注意，數字較高表示優先順序較低。</span><span class="sxs-lookup"><span data-stu-id="57f13-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="57f13-261">根據預設，此值會設定為 1，這是最高的優先順序。</span><span class="sxs-lookup"><span data-stu-id="57f13-261">By default, this is set to 1, which is the highest possible priority.</span></span>

<span data-ttu-id="57f13-262">每個帳戶都已設定預設原則。</span><span class="sxs-lookup"><span data-stu-id="57f13-262">There is a default policy set on every account.</span></span> <span data-ttu-id="57f13-263">預設原則會套用到帳戶的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="57f13-263">The default policy applies to all users of the account.</span></span> <span data-ttu-id="57f13-264">您可以針對特定使用者和群組設定其他原則。</span><span class="sxs-lookup"><span data-stu-id="57f13-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="57f13-265">帳戶層級原則和作業層級原則可同時套用。</span><span class="sxs-lookup"><span data-stu-id="57f13-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="57f13-266">新增特定使用者或群組的原則</span><span class="sxs-lookup"><span data-stu-id="57f13-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="57f13-267">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-267">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-268">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-268">Click **Properties**.</span></span>
3. <span data-ttu-id="57f13-269">在 [作業提交限制] 之下，按一下 [新增原則] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="57f13-269">Under **Job Submission Limits**, click the **Add Policy** button.</span></span> <span data-ttu-id="57f13-270">然後，選取或輸入下列設定：</span><span class="sxs-lookup"><span data-stu-id="57f13-270">Then, select or enter the following settings:</span></span>
    1. <span data-ttu-id="57f13-271">**計算原則名稱**：輸入原則名稱，藉此提醒您原則的用途。</span><span class="sxs-lookup"><span data-stu-id="57f13-271">**Compute Policy Name**: Enter a policy name, to remind you of the purpose of the policy.</span></span>
    2. <span data-ttu-id="57f13-272">**選取使用者或群組**：選取適用此原則的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="57f13-272">**Select User or Group**: Select the user or group this policy applies to.</span></span>
    3. <span data-ttu-id="57f13-273">**設定作業 AU 限制**：設定會套用到所選使用者或群組的 AU 限制。</span><span class="sxs-lookup"><span data-stu-id="57f13-273">**Set the Job AU Limit**: Set the AU limit that applies to the selected user or group.</span></span>
    4. <span data-ttu-id="57f13-274">**設定優先順序限制**：設定會套用所選使用者或群組的優先順序限制。</span><span class="sxs-lookup"><span data-stu-id="57f13-274">**Set the Priority Limit**: Set the priority limit that applies to the selected user or group.</span></span>

4. <span data-ttu-id="57f13-275">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="57f13-275">Click **Ok**.</span></span>

5. <span data-ttu-id="57f13-276">新原則會列在 [預設] 原則資料表的 [作業提交限制] 之下。</span><span class="sxs-lookup"><span data-stu-id="57f13-276">The new policy is listed in the **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="57f13-277">刪除或編輯現有原則</span><span class="sxs-lookup"><span data-stu-id="57f13-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="57f13-278">在 Azure 入口網站中，移至您的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57f13-278">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="57f13-279">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="57f13-279">Click **Properties**.</span></span>
3. <span data-ttu-id="57f13-280">在 [作業提交限制] 之下，尋找您想要編輯的原則。</span><span class="sxs-lookup"><span data-stu-id="57f13-280">Under **Job Submission Limits**, find the policy you want to edit.</span></span>
4.  <span data-ttu-id="57f13-281">若要查看 [刪除] 和 [編輯] 選項，請在資料表的最右邊資料行中，按一下 [...]。</span><span class="sxs-lookup"><span data-stu-id="57f13-281">To see the **Delete** and **Edit** options, in the rightmost column of the table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="57f13-282">作業原則的其他資源</span><span class="sxs-lookup"><span data-stu-id="57f13-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="57f13-283">原則概觀部落格文章</span><span class="sxs-lookup"><span data-stu-id="57f13-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="57f13-284">帳戶層級原則部落格文章</span><span class="sxs-lookup"><span data-stu-id="57f13-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="57f13-285">作業層級原則部落格文章</span><span class="sxs-lookup"><span data-stu-id="57f13-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="57f13-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57f13-286">Next steps</span></span>

* [<span data-ttu-id="57f13-287">Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="57f13-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="57f13-288">使用 Azure 入口網站開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="57f13-288">Get started with Data Lake Analytics by using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="57f13-289">使用 Azure PowerShell 管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="57f13-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

