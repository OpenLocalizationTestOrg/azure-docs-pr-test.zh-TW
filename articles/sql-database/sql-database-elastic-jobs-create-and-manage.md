---
title: "Azure SQL 資料庫 aaaManage 群組 |Microsoft 文件"
description: "逐步解說如何建立和管理彈性工作。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="f463a-103">使用彈性工作建立和管理相應放大的 Azure SQL Database (預覽)</span><span class="sxs-lookup"><span data-stu-id="f463a-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="f463a-104">**彈性資料庫工作** 可以簡化資料庫群組的管理，方法是執行系統管理作業 (例如結構描述變更、認證管理、參考資料更新、效能資料收集，或租用戶 (客戶) 遙測收集)。</span><span class="sxs-lookup"><span data-stu-id="f463a-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="f463a-105">彈性資料庫工作是目前可透過 Azure 入口網站 hello 和 PowerShell 指令程式。</span><span class="sxs-lookup"><span data-stu-id="f463a-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="f463a-106">不過，hello Azure 入口網站介面的功能會減少受限於 tooexecution 中的所有資料庫[彈性集區 （預覽）](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="f463a-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="f463a-107">tooaccess 額外的功能和執行指令碼一整組資料庫包括自訂的集合或分區設定 (使用建立[彈性資料庫用戶端程式庫](sql-database-elastic-scale-introduction.md))，請參閱[建立和管理作業使用 PowerShell](sql-database-elastic-jobs-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="f463a-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="f463a-108">如需工作的詳細資訊，請參閱 [彈性資料庫工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f463a-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f463a-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="f463a-109">Prerequisites</span></span>
* <span data-ttu-id="f463a-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f463a-110">An Azure subscription.</span></span> <span data-ttu-id="f463a-111">如需免費試用版，請參閱 [免費試用版](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f463a-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f463a-112">彈性集區。</span><span class="sxs-lookup"><span data-stu-id="f463a-112">An elastic pool.</span></span> <span data-ttu-id="f463a-113">請參閱[關於彈性集區](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="f463a-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="f463a-114">安裝彈性資料庫工作服務元件。</span><span class="sxs-lookup"><span data-stu-id="f463a-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="f463a-115">請參閱[安裝 hello 彈性資料庫工作服務](sql-database-elastic-jobs-service-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="f463a-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="f463a-116">建立工作 (Job)</span><span class="sxs-lookup"><span data-stu-id="f463a-116">Creating jobs</span></span>
1. <span data-ttu-id="f463a-117">使用 hello [Azure 入口網站](https://portal.azure.com)，從現有的彈性資料庫工作集區，按一下 **建立工作**。</span><span class="sxs-lookup"><span data-stu-id="f463a-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="f463a-118">輸入 hello 使用者名稱和密碼的 hello （建立在安裝作業） 的資料庫管理員在 hello 工作控制資料庫 （作業的中繼資料儲存體）。</span><span class="sxs-lookup"><span data-stu-id="f463a-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![名稱 hello 工作，輸入或貼上程式碼，然後按一下 [執行]][1]
3. <span data-ttu-id="f463a-120">在 hello**建立作業**刀鋒視窗中，輸入 hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="f463a-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="f463a-121">輸入 hello 使用者名稱和密碼 tooconnect toohello 目標資料庫有足夠的權限的指令碼執行 toosucceed。</span><span class="sxs-lookup"><span data-stu-id="f463a-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="f463a-122">貼上或輸入 hello T-SQL 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="f463a-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="f463a-123">按一下 儲存，然後按一下執行。</span><span class="sxs-lookup"><span data-stu-id="f463a-123">Click **Save** and then click **Run**.</span></span>
   
    ![建立工作並執行][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="f463a-125">執行等冪工作</span><span class="sxs-lookup"><span data-stu-id="f463a-125">Run idempotent jobs</span></span>
<span data-ttu-id="f463a-126">當您針對一組資料庫中執行指令碼時，您必須確定 hello 指令碼為等冪。</span><span class="sxs-lookup"><span data-stu-id="f463a-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="f463a-127">也就是 hello 指令碼必須能夠 toorun 許多次，即使它失敗之前處於未完成的狀態。</span><span class="sxs-lookup"><span data-stu-id="f463a-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="f463a-128">例如，指令碼失敗時，hello 作業將自動重試直到成功為止 （限制範圍內，為 hello 重試邏輯將最終停止 hello 重試一次）。</span><span class="sxs-lookup"><span data-stu-id="f463a-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="f463a-129">hello 方式 toodo 這是 toouse hello 「 如果存在 」 的子句，建立新的物件之前先刪除任何找到的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f463a-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="f463a-130">範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="f463a-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="f463a-131">或者，使用 "IF NOT EXISTS" 子句，再建立新的執行個體：</span><span class="sxs-lookup"><span data-stu-id="f463a-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="f463a-132">此指令碼，然後更新 hello 先前建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="f463a-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="f463a-133">檢查工作狀態</span><span class="sxs-lookup"><span data-stu-id="f463a-133">Checking job status</span></span>
<span data-ttu-id="f463a-134">工作開始之後，您可以檢查它的進度。</span><span class="sxs-lookup"><span data-stu-id="f463a-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="f463a-135">從 hello 彈性集區] 頁面上，按一下 [**管理工作**。</span><span class="sxs-lookup"><span data-stu-id="f463a-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![按一下 [管理工作]][2]
2. <span data-ttu-id="f463a-137">按一下 hello (a) 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="f463a-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="f463a-138">hello**狀態**可以是 「 已完成 」 或 「 失敗 」。</span><span class="sxs-lookup"><span data-stu-id="f463a-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="f463a-139">hello 工作的詳細資料會出現 (b) 的日期和時間建立和執行。</span><span class="sxs-lookup"><span data-stu-id="f463a-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="f463a-140">以下顯示 hello 進度 hello 指令碼的每個資料庫中 hello 集區，提供其日期和時間的詳細資料的 hello hello 清單 (c)。</span><span class="sxs-lookup"><span data-stu-id="f463a-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![檢查完成的工作][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="f463a-142">檢查失敗的工作</span><span class="sxs-lookup"><span data-stu-id="f463a-142">Checking failed jobs</span></span>
<span data-ttu-id="f463a-143">如果工作失敗，您可以找到其執行記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f463a-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="f463a-144">按一下 hello 失敗作業 toosee hello 名稱其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f463a-144">Click hello name of hello failed job toosee its details.</span></span>

![查看失敗的工作][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


