---
title: "管理 Azure SQL Database 的群組 | Microsoft Docs"
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
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="ddbcd-103">使用彈性工作建立和管理相應放大的 Azure SQL Database (預覽)</span><span class="sxs-lookup"><span data-stu-id="ddbcd-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="ddbcd-104">**彈性資料庫工作** 可以簡化資料庫群組的管理，方法是執行系統管理作業 (例如結構描述變更、認證管理、參考資料更新、效能資料收集，或租用戶 (客戶) 遙測收集)。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="ddbcd-105">彈性資料庫工作目前可透過 Azure 入口網站和 PowerShell Cmdlet 使用。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="ddbcd-106">不過，Azure 入口網站呈現精簡功能會限制為跨[彈性集區 (預覽)](sql-database-elastic-pool.md) 中的所有資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="ddbcd-107">若要存取其他功能以及跨資料庫群組執行指令碼，包括自訂定義集合或分區集 (使用[彈性資料庫用戶端程式庫](sql-database-elastic-scale-introduction.md)建立)，請參閱[使用 PowerShell 建立和管理作業](sql-database-elastic-jobs-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="ddbcd-108">如需工作的詳細資訊，請參閱 [彈性資料庫工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ddbcd-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="ddbcd-109">Prerequisites</span></span>
* <span data-ttu-id="ddbcd-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-110">An Azure subscription.</span></span> <span data-ttu-id="ddbcd-111">如需免費試用版，請參閱 [免費試用版](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ddbcd-112">彈性集區。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-112">An elastic pool.</span></span> <span data-ttu-id="ddbcd-113">請參閱[關於彈性集區](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="ddbcd-114">安裝彈性資料庫工作服務元件。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="ddbcd-115">請參閱 [安裝彈性資料庫工作服務](sql-database-elastic-jobs-service-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="ddbcd-116">建立工作 (Job)</span><span class="sxs-lookup"><span data-stu-id="ddbcd-116">Creating jobs</span></span>
1. <span data-ttu-id="ddbcd-117">使用 [Azure 入口網站](https://portal.azure.com)，從現有的彈性資料庫工作集區，按一下 [建立作業]。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="ddbcd-118">輸入工作控制資料庫 (工作的中繼資料儲存體) 之資料庫系統管理員 (在安裝工作時建立) 的使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![為工作命名，輸入或貼上程式碼，然後按一下 [執行]][1]
3. <span data-ttu-id="ddbcd-120">在 [建立工作]  刀鋒視窗中，輸入工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="ddbcd-121">輸入使用者名稱與密碼來連線至目標資料庫，以取得足夠權限來成功執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="ddbcd-122">貼上或輸入 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="ddbcd-123">按一下 [儲存]，然後按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-123">Click **Save** and then click **Run**.</span></span>
   
    ![建立工作並執行][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="ddbcd-125">執行等冪工作</span><span class="sxs-lookup"><span data-stu-id="ddbcd-125">Run idempotent jobs</span></span>
<span data-ttu-id="ddbcd-126">當您對一組資料庫執行指令碼時，您必須確定指令碼是等冪。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="ddbcd-127">換句話說，指令碼必須能夠重複執行，即使之前在未完成狀態失敗亦然。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="ddbcd-128">例如，當指令碼失敗時，系統會自動重試工作，直到成功為止 (在限制內，因為重試邏輯最終將會停止重試)。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="ddbcd-129">其作法是使用 "IF EXISTS" 子句，並刪除任何找到的執行個體，再建立新的物件。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="ddbcd-130">範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="ddbcd-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="ddbcd-131">或者，使用 "IF NOT EXISTS" 子句，再建立新的執行個體：</span><span class="sxs-lookup"><span data-stu-id="ddbcd-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="ddbcd-132">這個指令碼會接著更新之前建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="ddbcd-133">檢查工作狀態</span><span class="sxs-lookup"><span data-stu-id="ddbcd-133">Checking job status</span></span>
<span data-ttu-id="ddbcd-134">工作開始之後，您可以檢查它的進度。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="ddbcd-135">從 [彈性集區] 頁面，按一下 [管理工作]。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    ![按一下 [管理工作]][2]
2. <span data-ttu-id="ddbcd-137">按一下工作的名稱 (a)。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="ddbcd-138">[狀態]  可以是 [已完成] 或 [失敗]。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="ddbcd-139">工作的詳細資料隨即出現 (b)，並提供建立和執行的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="ddbcd-140">其下方的清單 (c) 顯示對集區中每個資料庫執行指令碼的進度，並提供其日期和時間詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![檢查完成的工作][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="ddbcd-142">檢查失敗的工作</span><span class="sxs-lookup"><span data-stu-id="ddbcd-142">Checking failed jobs</span></span>
<span data-ttu-id="ddbcd-143">如果工作失敗，您可以找到其執行記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="ddbcd-144">按一下失敗工作的名稱，以查看其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddbcd-144">Click the name of the failed job to see its details.</span></span>

![查看失敗的工作][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


