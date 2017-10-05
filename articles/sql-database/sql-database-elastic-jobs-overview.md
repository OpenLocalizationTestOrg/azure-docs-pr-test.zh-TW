---
title: "管理相應放大的雲端資料庫 | Microsoft Docs"
description: "說明彈性資料庫工作服務"
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8e84562115a866c0df5e0dee6c7f66c036a74737
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-scaled-out-cloud-databases"></a><span data-ttu-id="0c8de-103">管理相應放大的雲端資料庫</span><span class="sxs-lookup"><span data-stu-id="0c8de-103">Managing scaled-out cloud databases</span></span>
<span data-ttu-id="0c8de-104">若要管理相應放大的共用資料庫，**彈性資料庫作業**功能 (預覽) 可讓您在一組資料庫中可靠地執行 TRANSACT-SQL (T-SQL) 指令碼，其中包括：</span><span class="sxs-lookup"><span data-stu-id="0c8de-104">To manage scaled-out sharded databases, the **Elastic Database jobs** feature (preview) enables you to reliably execute a Transact-SQL (T-SQL) script across a group of databases, including:</span></span>

* <span data-ttu-id="0c8de-105">自訂的資料庫集合 (如下所述)</span><span class="sxs-lookup"><span data-stu-id="0c8de-105">a custom-defined collection of databases (explained below)</span></span>
* <span data-ttu-id="0c8de-106">[彈性集區](sql-database-elastic-pool.md)中的所有資料庫</span><span class="sxs-lookup"><span data-stu-id="0c8de-106">all databases in an [elastic pool](sql-database-elastic-pool.md)</span></span>
* <span data-ttu-id="0c8de-107">分區集 (使用 [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)建立)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-107">a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> 

## <a name="documentation"></a><span data-ttu-id="0c8de-108">文件</span><span class="sxs-lookup"><span data-stu-id="0c8de-108">Documentation</span></span>
* <span data-ttu-id="0c8de-109">[安裝彈性資料庫工作元件](sql-database-elastic-jobs-service-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-109">[Install the Elastic Database job components](sql-database-elastic-jobs-service-installation.md).</span></span> 
* <span data-ttu-id="0c8de-110">[開始使用彈性資料庫工作](sql-database-elastic-jobs-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-110">[Get started with Elastic Database jobs](sql-database-elastic-jobs-getting-started.md).</span></span>
* <span data-ttu-id="0c8de-111">[使用 Powershell 建立和管理工作](sql-database-elastic-jobs-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-111">[Create and manage jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span>
* [<span data-ttu-id="0c8de-112">建立和管理相應放大的 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0c8de-112">Create and manage scaled out Azure SQL Databases</span></span>](sql-database-elastic-jobs-getting-started.md)

<span data-ttu-id="0c8de-113">**彈性資料庫作業**目前是客戶裝載的 Azure 雲端服務，可以執行臨機操作和排程的管理作業，稱為**作業**。</span><span class="sxs-lookup"><span data-stu-id="0c8de-113">**Elastic Database jobs** is currently a customer-hosted Azure Cloud Service that enables the execution of ad-hoc and scheduled administrative tasks, which are called **jobs**.</span></span> <span data-ttu-id="0c8de-114">利用工作，您可以執行 Transact-SQL 指令碼來執行管理作業，進而輕鬆又可靠地管理大量 Azure SQL Database 群組。</span><span class="sxs-lookup"><span data-stu-id="0c8de-114">With jobs, you can easily and reliably manage large groups of Azure SQL Databases by running Transact-SQL scripts to perform administrative operations.</span></span> 

![彈性資料庫工作服務][1]

## <a name="why-use-jobs"></a><span data-ttu-id="0c8de-116">為何要使用工作？</span><span class="sxs-lookup"><span data-stu-id="0c8de-116">Why use jobs?</span></span>
<span data-ttu-id="0c8de-117">**管理**</span><span class="sxs-lookup"><span data-stu-id="0c8de-117">**Manage**</span></span>

<span data-ttu-id="0c8de-118">輕鬆執行結構描述變更、認證管理、參考資料更新、效能資料收集，或租用戶 (客戶) 遙測收集。</span><span class="sxs-lookup"><span data-stu-id="0c8de-118">Easily do schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span>

<span data-ttu-id="0c8de-119">**報告**</span><span class="sxs-lookup"><span data-stu-id="0c8de-119">**Reports**</span></span>

<span data-ttu-id="0c8de-120">將 Azure SQL Database 集合中的資料彙總到單一目的地資料表中。</span><span class="sxs-lookup"><span data-stu-id="0c8de-120">Aggregate data from a collection of Azure SQL Databases into a single destination table.</span></span>

<span data-ttu-id="0c8de-121">**減少額外負荷**</span><span class="sxs-lookup"><span data-stu-id="0c8de-121">**Reduce overhead**</span></span>

<span data-ttu-id="0c8de-122">通常，您必須個別連接到每個資料庫，以執行 Transact-SQL 陳述式或執行其他管理工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-122">Normally, you must connect to each database independently in order to run Transact-SQL statements or perform other administrative tasks.</span></span> <span data-ttu-id="0c8de-123">工作會處理登入目標群組中每個資料庫的工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-123">A job handles the task of logging in to each database in the target group.</span></span> <span data-ttu-id="0c8de-124">您也要定義、維護及保存要在 Azure SQL Database 的群組中執行的 Transact-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0c8de-124">You also define, maintain and persist Transact-SQL scripts to be executed across a group of Azure SQL Databases.</span></span>

<span data-ttu-id="0c8de-125">**資料記錄**</span><span class="sxs-lookup"><span data-stu-id="0c8de-125">**Accounting**</span></span>

<span data-ttu-id="0c8de-126">工作會執行指令碼並記錄每個資料庫的執行狀態。</span><span class="sxs-lookup"><span data-stu-id="0c8de-126">Jobs run the script and log the status of execution for each database.</span></span> <span data-ttu-id="0c8de-127">失敗時也會自動重試。</span><span class="sxs-lookup"><span data-stu-id="0c8de-127">You also get automatic retry when failures occur.</span></span>

<span data-ttu-id="0c8de-128">**彈性**</span><span class="sxs-lookup"><span data-stu-id="0c8de-128">**Flexibility**</span></span>

<span data-ttu-id="0c8de-129">定義 Azure SQL Database 的自訂群組，並定義排程以執行工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-129">Define custom groups of Azure SQL Databases, and define schedules for running a job.</span></span>

> [!NOTE]
> <span data-ttu-id="0c8de-130">在 Azure 入口網站中，只有一小組受限為 SQL Azure 彈性集區的函式可供使用。</span><span class="sxs-lookup"><span data-stu-id="0c8de-130">In the Azure portal, only a reduced set of functions limited to SQL Azure elastic pools is available.</span></span> <span data-ttu-id="0c8de-131">使用 PowerShell API 來存取目前功能的完整集合。</span><span class="sxs-lookup"><span data-stu-id="0c8de-131">Use the PowerShell APIs to access the full set of current functionality.</span></span>
> 
> 

## <a name="applications"></a><span data-ttu-id="0c8de-132">應用程式</span><span class="sxs-lookup"><span data-stu-id="0c8de-132">Applications</span></span>
* <span data-ttu-id="0c8de-133">執行管理工作，例如部署新的結構描述。</span><span class="sxs-lookup"><span data-stu-id="0c8de-133">Perform administrative tasks, such as deploying a new schema.</span></span>
* <span data-ttu-id="0c8de-134">更新所有資料庫通用的產品資料參考資訊。</span><span class="sxs-lookup"><span data-stu-id="0c8de-134">Update reference data-product information common across all databases.</span></span> <span data-ttu-id="0c8de-135">或排程每個工作日數小時後的自動更新。</span><span class="sxs-lookup"><span data-stu-id="0c8de-135">Or schedules automatic updates every weekday, after hours.</span></span>
* <span data-ttu-id="0c8de-136">重建索引以提升查詢效能。</span><span class="sxs-lookup"><span data-stu-id="0c8de-136">Rebuild indexes to improve query performance.</span></span> <span data-ttu-id="0c8de-137">重建作業可以設定為以週期性基礎跨資料庫的集合執行，例如在離峰時段。</span><span class="sxs-lookup"><span data-stu-id="0c8de-137">The rebuilding can be configured to execute across a collection of databases on a recurring basis, such as during off-peak hours.</span></span>
* <span data-ttu-id="0c8de-138">以持續執行的基礎從一組資料庫將查詢結果收集至中央資料表。</span><span class="sxs-lookup"><span data-stu-id="0c8de-138">Collect query results from a set of databases into a central table on an on-going basis.</span></span> <span data-ttu-id="0c8de-139">效能查詢可以持續執行，並設定為觸發要執行的其他作業。</span><span class="sxs-lookup"><span data-stu-id="0c8de-139">Performance queries can be continually executed and configured to trigger additional tasks to be executed.</span></span>
* <span data-ttu-id="0c8de-140">跨大型資料庫集合執行較長的執行資料處理查詢，例如客戶遙測的集合。</span><span class="sxs-lookup"><span data-stu-id="0c8de-140">Execute longer running data processing queries across a large set of databases, for example the collection of customer telemetry.</span></span> <span data-ttu-id="0c8de-141">結果會收集到單一目的地資料表做進一步的分析。</span><span class="sxs-lookup"><span data-stu-id="0c8de-141">Results are collected into a single destination table for further analysis.</span></span>

## <a name="elastic-database-jobs-end-to-end"></a><span data-ttu-id="0c8de-142">彈性資料庫工作：端對端</span><span class="sxs-lookup"><span data-stu-id="0c8de-142">Elastic Database jobs: end-to-end</span></span>
1. <span data-ttu-id="0c8de-143">安裝 **彈性資料庫工作** 元件。</span><span class="sxs-lookup"><span data-stu-id="0c8de-143">Install the **Elastic Database jobs** components.</span></span> <span data-ttu-id="0c8de-144">如需詳細資訊，請參閱 [安裝彈性資料庫工作](sql-database-elastic-jobs-service-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-144">For more information, see [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md).</span></span> <span data-ttu-id="0c8de-145">如果安裝失敗，請參閱 [如何解除安裝](sql-database-elastic-jobs-uninstall.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-145">If the installation fails, see [how to uninstall](sql-database-elastic-jobs-uninstall.md).</span></span>
2. <span data-ttu-id="0c8de-146">使用 PowerShell API 來存取更多功能，例如建立自訂定義資料庫集合、新增排程及/或收集結果集。</span><span class="sxs-lookup"><span data-stu-id="0c8de-146">Use the PowerShell APIs to access more functionality, for example creating custom-defined database collections, adding schedules and/or gathering results sets.</span></span> <span data-ttu-id="0c8de-147">使用入口網站來進行簡單安裝，以及建立/監視僅限針對「彈性集區」執行的工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-147">Use the portal for simple installation and creation/monitoring of jobs limited to execution against a **elastic pool**.</span></span> 
3. <span data-ttu-id="0c8de-148">針對工作執行建立加密認證及 [將使用者 (或角色) 新增至群組中的每個資料庫](sql-database-security-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-148">Create encrypted credentials for job execution and [add the user (or role) to each database in the group](sql-database-security-overview.md).</span></span>
4. <span data-ttu-id="0c8de-149">建立能夠針對群組中的每個資料庫執行的等冪 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0c8de-149">Create an idempotent T-SQL script that can be run against every database in the group.</span></span> 
5. <span data-ttu-id="0c8de-150">遵循下列步驟，使用 Azure 入口網站建立工作： [建立和管理彈性資料庫工作](sql-database-elastic-jobs-create-and-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-150">Follow these steps to create jobs using the Azure portal: [Creating and managing Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md).</span></span> 
6. <span data-ttu-id="0c8de-151">或使用 PowerShell 指令碼： [使用 PowerShell 建立和管理 SQL Database 彈性資料庫工作 (預覽)](sql-database-elastic-jobs-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-151">Or use PowerShell scripts: [Create and manage a SQL Database elastic database jobs using PowerShell (preview)](sql-database-elastic-jobs-powershell.md).</span></span>

## <a name="idempotent-scripts"></a><span data-ttu-id="0c8de-152">等冪指令碼</span><span class="sxs-lookup"><span data-stu-id="0c8de-152">Idempotent scripts</span></span>
<span data-ttu-id="0c8de-153">指令碼必須 [具有等冪性](https://en.wikipedia.org/wiki/Idempotence)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-153">The scripts must be [idempotent](https://en.wikipedia.org/wiki/Idempotence).</span></span> <span data-ttu-id="0c8de-154">簡單地說，「等冪」表示如果指令碼成功，而且再次執行，就會出現相同的結果。</span><span class="sxs-lookup"><span data-stu-id="0c8de-154">In simple terms, "idempotent" means that if the script succeeds, and it is run again, the same result occurs.</span></span> <span data-ttu-id="0c8de-155">指令碼可能會因為暫時性網路問題而失敗。</span><span class="sxs-lookup"><span data-stu-id="0c8de-155">A script may fail due to transient network issues.</span></span> <span data-ttu-id="0c8de-156">在此情況下，工作會自動重新執行指令碼，達到預設的次數才會停止。</span><span class="sxs-lookup"><span data-stu-id="0c8de-156">In that case, the job will automatically retry running the script a preset number of times before desisting.</span></span> <span data-ttu-id="0c8de-157">即使等冪指令碼已成功執行兩次，仍會有相同的結果。</span><span class="sxs-lookup"><span data-stu-id="0c8de-157">An idempotent script has the same result even if has been successfully run twice.</span></span> 

<span data-ttu-id="0c8de-158">簡單的策略是在建立物件之前，測試其是否存在。</span><span class="sxs-lookup"><span data-stu-id="0c8de-158">A simple tactic is to test for the existence of an object before creating it.</span></span>  

    IF NOT EXIST (some_object)
    -- Create the object 
    -- If it exists, drop the object before recreating it.

<span data-ttu-id="0c8de-159">同樣地，指令碼必須以邏輯方式測試並反駁它所找到的任何條件，才能夠順利執行。</span><span class="sxs-lookup"><span data-stu-id="0c8de-159">Similarly, a script must be able to execute successfully by logically testing for and countering any conditions it finds.</span></span>

## <a name="failures-and-logs"></a><span data-ttu-id="0c8de-160">失敗和記錄檔</span><span class="sxs-lookup"><span data-stu-id="0c8de-160">Failures and logs</span></span>
<span data-ttu-id="0c8de-161">如果指令碼在多次嘗試之後失敗，工作就會記錄錯誤並繼續。</span><span class="sxs-lookup"><span data-stu-id="0c8de-161">If a script fails after multiple attempts, the job logs the error and continues.</span></span> <span data-ttu-id="0c8de-162">在工作結束後 (亦即針對群組中的所有資料庫執行)，您可以檢查其失敗的嘗試清單。</span><span class="sxs-lookup"><span data-stu-id="0c8de-162">After a job ends (meaning a run against all databases in the group), you can check its list of failed attempts.</span></span> <span data-ttu-id="0c8de-163">記錄檔會提供詳細資料以偵錯錯誤的指令碼。</span><span class="sxs-lookup"><span data-stu-id="0c8de-163">The logs provide details to debug faulty scripts.</span></span> 

## <a name="group-types-and-creation"></a><span data-ttu-id="0c8de-164">群組類型和建立</span><span class="sxs-lookup"><span data-stu-id="0c8de-164">Group types and creation</span></span>
<span data-ttu-id="0c8de-165">群組有兩種：</span><span class="sxs-lookup"><span data-stu-id="0c8de-165">There are two kinds of groups:</span></span> 

1. <span data-ttu-id="0c8de-166">分區集</span><span class="sxs-lookup"><span data-stu-id="0c8de-166">Shard sets</span></span>
2. <span data-ttu-id="0c8de-167">自訂群組</span><span class="sxs-lookup"><span data-stu-id="0c8de-167">Custom groups</span></span>

<span data-ttu-id="0c8de-168">分區集群組是使用 [彈性資料庫工具](sql-database-elastic-scale-introduction.md)所建立。</span><span class="sxs-lookup"><span data-stu-id="0c8de-168">Shard set groups are created using the [Elastic Database tools](sql-database-elastic-scale-introduction.md).</span></span> <span data-ttu-id="0c8de-169">當您建立分區集群組時，會在群組中自動加入或移除資料庫。</span><span class="sxs-lookup"><span data-stu-id="0c8de-169">When you create a shard set group, databases are added or removed from the group automatically.</span></span> <span data-ttu-id="0c8de-170">例如，當您將它加入分區對應中時，新的分區就會自動加入群組中。</span><span class="sxs-lookup"><span data-stu-id="0c8de-170">For example, a new shard will be automatically in the group when you add it to the shard map.</span></span> <span data-ttu-id="0c8de-171">然後就可以對群組執行工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-171">A job can then be run against the group.</span></span>

<span data-ttu-id="0c8de-172">另一方面，自訂群組的定義方式很嚴格。</span><span class="sxs-lookup"><span data-stu-id="0c8de-172">Custom groups, on the other hand, are rigidly defined.</span></span> <span data-ttu-id="0c8de-173">您必須在自訂群組中明確地加入或移除資料庫。</span><span class="sxs-lookup"><span data-stu-id="0c8de-173">You must explicitly add or remove databases from custom groups.</span></span> <span data-ttu-id="0c8de-174">如果群組中的資料庫已遭刪除，工作會嘗試對最終導致失敗的資料庫執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="0c8de-174">If a database in the group is dropped, the job will attempt to run the script against the database resulting in an eventual failure.</span></span> <span data-ttu-id="0c8de-175">使用 Azure 入口網站建立的群組目前是自訂群組。</span><span class="sxs-lookup"><span data-stu-id="0c8de-175">Groups created using the Azure portal currently are custom groups.</span></span> 

## <a name="components-and-pricing"></a><span data-ttu-id="0c8de-176">元件和價格</span><span class="sxs-lookup"><span data-stu-id="0c8de-176">Components and pricing</span></span>
<span data-ttu-id="0c8de-177">下列元件共同建立允許臨機執行管理工作的 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0c8de-177">The following components work together to create an Azure Cloud service that enables ad-hoc execution of administrative jobs.</span></span> <span data-ttu-id="0c8de-178">這些元件會於安裝期間在您的訂用帳戶中自動安裝和設定。</span><span class="sxs-lookup"><span data-stu-id="0c8de-178">The components are installed and configured automatically during setup, in your subscription.</span></span> <span data-ttu-id="0c8de-179">您可以識別服務，因為這些服務都有自動產生的相同名稱。</span><span class="sxs-lookup"><span data-stu-id="0c8de-179">You can identify the services as they all have the same auto-generated name.</span></span> <span data-ttu-id="0c8de-180">這個名稱是唯一的，包含前置詞 "edj"，後面接著隨機產生的 21 個字元。</span><span class="sxs-lookup"><span data-stu-id="0c8de-180">The name is unique, and consists of the prefix "edj" followed by 21 randomly generated characters.</span></span>

* <span data-ttu-id="0c8de-181">**Azure 雲端服務**：彈性資料庫工作 (預覽) 會以客戶託管的 Azure 雲端服務來傳遞，以執行所要求的工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-181">**Azure Cloud Service**: elastic database jobs (preview) is delivered as a customer-hosted Azure Cloud service to perform execution of the requested tasks.</span></span> <span data-ttu-id="0c8de-182">您可以從入口網站，在 Microsoft Azure 訂用帳戶中部署及託管服務。</span><span class="sxs-lookup"><span data-stu-id="0c8de-182">From the portal, the service is deployed and hosted in your Microsoft Azure subscription.</span></span> <span data-ttu-id="0c8de-183">預設至少會使用兩個背景工作角色來執行已部署的服務，以取得高可用性。</span><span class="sxs-lookup"><span data-stu-id="0c8de-183">The default deployed service runs with the minimum of two worker roles for high availability.</span></span> <span data-ttu-id="0c8de-184">每個背景工作角色 (ElasticDatabaseJobWorker) 都會以預設大小在 A0 執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="0c8de-184">The default size of each worker role (ElasticDatabaseJobWorker) runs on an A0 instance.</span></span> <span data-ttu-id="0c8de-185">如需價格，請參閱 [雲端服務價格](https://azure.microsoft.com/pricing/details/cloud-services/)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-185">For pricing, see [Cloud services pricing](https://azure.microsoft.com/pricing/details/cloud-services/).</span></span> 
* <span data-ttu-id="0c8de-186">**Azure SQL Database**：服務會使用稱為**控制資料庫**的 Azure SQL Database 來儲存所有的工作中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0c8de-186">**Azure SQL Database**: The service uses an Azure SQL Database known as the **control database** to store all of the job metadata.</span></span> <span data-ttu-id="0c8de-187">預設服務層為 S0。</span><span class="sxs-lookup"><span data-stu-id="0c8de-187">The default service tier is a S0.</span></span> <span data-ttu-id="0c8de-188">如需價格，請參閱 [SQL Database 價格](https://azure.microsoft.com/pricing/details/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-188">For pricing, see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>
* <span data-ttu-id="0c8de-189">**Azure 服務匯流排**：Azure 服務匯流排可協調 Azure 雲端服務內的工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-189">**Azure Service Bus**: An Azure Service Bus is for coordination of the work within the Azure Cloud Service.</span></span> <span data-ttu-id="0c8de-190">請參閱 [服務匯流排價格](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-190">See [Service Bus Pricing](https://azure.microsoft.com/pricing/details/service-bus/).</span></span>
* <span data-ttu-id="0c8de-191">**Azure 儲存體**：Azure 儲存體帳戶可用來儲存在問題需要進一步偵錯的事件中所記錄的診斷輸出 (請參閱 [在 Azure 雲端服務和虛擬機器中啟用診斷](../cloud-services/cloud-services-dotnet-diagnostics.md))。</span><span class="sxs-lookup"><span data-stu-id="0c8de-191">**Azure Storage**: An Azure Storage account is used to store diagnostic output logging in the event that an issue requires further debugging (see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../cloud-services/cloud-services-dotnet-diagnostics.md)).</span></span> <span data-ttu-id="0c8de-192">如需價格，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-192">For pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-elastic-database-jobs-work"></a><span data-ttu-id="0c8de-193">彈性資料庫工作的運作方式</span><span class="sxs-lookup"><span data-stu-id="0c8de-193">How Elastic Database jobs work</span></span>
1. <span data-ttu-id="0c8de-194">Azure SQL Database 會指定 **控制資料庫** ，它會儲存所有中繼資料和狀態資料。</span><span class="sxs-lookup"><span data-stu-id="0c8de-194">An Azure SQL Database is designated a **control database** which stores all meta-data and state data.</span></span>
2. <span data-ttu-id="0c8de-195">控制資料庫是由 **工作服務** 存取，以啟動和追蹤要執行的工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-195">The control database is accessed by the **job service** to launch and track jobs to execute.</span></span>
3. <span data-ttu-id="0c8de-196">與控制資料庫通訊的兩個不同角色：</span><span class="sxs-lookup"><span data-stu-id="0c8de-196">Two different roles communicate with the control database:</span></span> 
   * <span data-ttu-id="0c8de-197">控制站：判斷哪些工作需要作業以執行要求的工作，並且藉由建立新的工作作業來重試失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-197">Controller: Determines which jobs require tasks to perform the requested job, and retries failed jobs by creating new job tasks.</span></span>
   * <span data-ttu-id="0c8de-198">工作作業執行：執行工作作業。</span><span class="sxs-lookup"><span data-stu-id="0c8de-198">Job Task Execution: Carries out the job tasks.</span></span>

### <a name="job-task-types"></a><span data-ttu-id="0c8de-199">工作作業類型</span><span class="sxs-lookup"><span data-stu-id="0c8de-199">Job task types</span></span>
<span data-ttu-id="0c8de-200">有多種類型的工作作業會執行工作：</span><span class="sxs-lookup"><span data-stu-id="0c8de-200">There are multiple types of job tasks that carry out execution of jobs:</span></span>

* <span data-ttu-id="0c8de-201">ShardMapRefresh：查詢分區對應來判斷做為分區的所有資料庫</span><span class="sxs-lookup"><span data-stu-id="0c8de-201">ShardMapRefresh: Queries the shard map to determine all the databases used as shards</span></span>
* <span data-ttu-id="0c8de-202">ScriptSplit：跨 ‘GO’ 陳述式將指令碼分割成批次</span><span class="sxs-lookup"><span data-stu-id="0c8de-202">ScriptSplit: Splits the script across ‘GO’ statements into batches</span></span>
* <span data-ttu-id="0c8de-203">ExpandJob：從以資料庫群組為目標的工作，針對每個資料庫建立子工作</span><span class="sxs-lookup"><span data-stu-id="0c8de-203">ExpandJob: Creates child jobs for each database from a job that targets a group of databases</span></span>
* <span data-ttu-id="0c8de-204">ScriptExecution：使用定義的認證針對特定資料庫執行指令碼</span><span class="sxs-lookup"><span data-stu-id="0c8de-204">ScriptExecution: Executes a script against a particular database using defined credentials</span></span>
* <span data-ttu-id="0c8de-205">Dacpac：使用特定認證將 DACPAC 套用至特定資料庫</span><span class="sxs-lookup"><span data-stu-id="0c8de-205">Dacpac: Applies a DACPAC to a particular database using particular credentials</span></span>

## <a name="end-to-end-job-execution-work-flow"></a><span data-ttu-id="0c8de-206">端對端工作執行工作流程</span><span class="sxs-lookup"><span data-stu-id="0c8de-206">End-to-end job execution work-flow</span></span>
1. <span data-ttu-id="0c8de-207">使用入口網站或 PowerShell API，工作會插入至**控制資料庫**。</span><span class="sxs-lookup"><span data-stu-id="0c8de-207">Using either the Portal or the PowerShell API, a job is inserted into the  **control database**.</span></span> <span data-ttu-id="0c8de-208">工作會使用特定認證，要求針對資料庫群組執行 Transact-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0c8de-208">The job requests execution of a Transact-SQL script against a group of databases using specific credentials.</span></span>
2. <span data-ttu-id="0c8de-209">控制站會識別新的工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-209">The controller identifies the new job.</span></span> <span data-ttu-id="0c8de-210">建立和執行工作作業以分割指令碼以及重新整理群組的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0c8de-210">Job tasks are created and executed to split the script and to refresh the group’s databases.</span></span> <span data-ttu-id="0c8de-211">最後，會建立和執行新的工作以展開作業，並且建立新的子工作，在其中指定每個子工作以根據群組中的個別資料庫執行 Transact-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0c8de-211">Lastly, a new job is created and executed to expand the job and create new child jobs where each child job is specified to execute the Transact-SQL script against an individual database in the group.</span></span>
3. <span data-ttu-id="0c8de-212">控制站會識別已建立的子工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-212">The controller identifies the created child jobs.</span></span> <span data-ttu-id="0c8de-213">對於每個工作，控制站會建立並觸發工作作業，以針對資料庫執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="0c8de-213">For each job, the controller creates and triggers a job task to execute the script against a database.</span></span> 
4. <span data-ttu-id="0c8de-214">完成所有工作作業之後，控制站會將工作更新為已完成狀態。</span><span class="sxs-lookup"><span data-stu-id="0c8de-214">After all job tasks have completed, the controller updates the jobs to a completed state.</span></span> 
   <span data-ttu-id="0c8de-215">在工作執行期間，可以隨時使用 PowerShell API 以檢視工作執行的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="0c8de-215">At any point during job execution, the PowerShell API can be used to view the current state of job execution.</span></span> <span data-ttu-id="0c8de-216">PowerShell API 所傳回的所有時間都是以 UTC 表示。</span><span class="sxs-lookup"><span data-stu-id="0c8de-216">All times returned by the PowerShell APIs are represented in UTC.</span></span> <span data-ttu-id="0c8de-217">如有需要，可以初始化取消要求以停止工作。</span><span class="sxs-lookup"><span data-stu-id="0c8de-217">If desired, a cancellation request can be initiated to stop a job.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0c8de-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c8de-218">Next steps</span></span>
<span data-ttu-id="0c8de-219">[安裝元件](sql-database-elastic-jobs-service-installation.md)，然後[建立記錄檔並加入資料庫群組中的每個資料庫](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-219">[Install the components](sql-database-elastic-jobs-service-installation.md), then [create and add a log in to each database in the group of databases](sql-database-manage-logins.md).</span></span> <span data-ttu-id="0c8de-220">若要進一步了解工作的建立和管理，請參閱 [建立及管理彈性資料庫工作](sql-database-elastic-jobs-create-and-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-220">To further understand job creation and management, see [creating and managing elastic database jobs](sql-database-elastic-jobs-create-and-manage.md).</span></span> <span data-ttu-id="0c8de-221">另請參閱 [開始使用彈性資料庫工作](sql-database-elastic-jobs-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0c8de-221">See also [Getting started with Elastic Database jobs](sql-database-elastic-jobs-getting-started.md).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


