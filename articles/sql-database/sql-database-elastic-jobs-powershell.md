---
title: "aaaCreate 及管理彈性的工作，使用 PowerShell |Microsoft 文件"
description: "使用 PowerShell toomanage Azure SQL Database 的集區"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="26de9-103">使用 PowerShell 建立和管理 SQL Database 彈性作業 (預覽)</span><span class="sxs-lookup"><span data-stu-id="26de9-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="26de9-104">hello PowerShell Api 的**彈性資料庫工作**（處於預覽階段），可讓您定義指令碼可執行針對這個資料庫的群組。</span><span class="sxs-lookup"><span data-stu-id="26de9-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="26de9-105">本文將說明如何 toocreate 和管理**彈性資料庫工作**使用 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="26de9-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="26de9-106">請參閱 [彈性工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="26de9-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="26de9-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="26de9-107">Prerequisites</span></span>
* <span data-ttu-id="26de9-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="26de9-108">An Azure subscription.</span></span> <span data-ttu-id="26de9-109">如需免費試用，請參閱 [免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="26de9-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="26de9-110">一組使用 hello 彈性資料庫工具所建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="26de9-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="26de9-111">請參閱 [開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="26de9-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="26de9-112">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="26de9-112">Azure PowerShell.</span></span> <span data-ttu-id="26de9-113">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="26de9-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="26de9-114">**彈性資料庫工作** PowerShell 封裝：請參閱 [安裝彈性資料庫工作](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="26de9-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="26de9-115">選取您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="26de9-115">Select your Azure subscription</span></span>
<span data-ttu-id="26de9-116">您需要您的訂用帳戶 Id tooselect hello 訂用帳戶 (**-SubscriptionId**) 或訂用帳戶名稱 (**-訂用帳戶名稱**)。</span><span class="sxs-lookup"><span data-stu-id="26de9-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="26de9-117">如果您有多個訂用帳戶，您就可以執行 hello **Get AzureRmSubscription** cmdlet，並複製 hello 預期從 hello 結果集的訂閱資訊。</span><span class="sxs-lookup"><span data-stu-id="26de9-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="26de9-118">訂用帳戶資訊之後，執行下列 commandlet tooset hello hello 預設為此訂用帳戶，也就是 hello 建立和管理作業的目標：</span><span class="sxs-lookup"><span data-stu-id="26de9-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="26de9-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx)使用量 toodevelop 建議，並執行 PowerShell 指令碼針對 hello 彈性資料庫工作。</span><span class="sxs-lookup"><span data-stu-id="26de9-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="26de9-120">彈性資料庫工作物件</span><span class="sxs-lookup"><span data-stu-id="26de9-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="26de9-121">下列表格列出所有 hello 物件類型的 hello**彈性資料庫工作**以及其描述和相關的 PowerShell Api。</span><span class="sxs-lookup"><span data-stu-id="26de9-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="26de9-122">物件類型</span><span class="sxs-lookup"><span data-stu-id="26de9-122">Object Type</span></span></th>
    <th><span data-ttu-id="26de9-123">說明</span><span class="sxs-lookup"><span data-stu-id="26de9-123">Description</span></span></th>
    <th><span data-ttu-id="26de9-124">相關 PowerShell API</span><span class="sxs-lookup"><span data-stu-id="26de9-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="26de9-125">認證</span><span class="sxs-lookup"><span data-stu-id="26de9-125">Credential</span></span></td>
    <td><span data-ttu-id="26de9-126">使用者名稱和密碼 toouse 連接執行的指令碼或應用程式的 Dacpac toodatabases 時。</span><span class="sxs-lookup"><span data-stu-id="26de9-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="26de9-127">hello 密碼是之前傳送 tooand hello 彈性資料庫工作的資料庫中儲存加密。</span><span class="sxs-lookup"><span data-stu-id="26de9-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="26de9-128">hello 密碼是由 hello 彈性資料庫工作服務，透過建立及上傳 hello 安裝指令碼中的 hello 認證解密。</span><span class="sxs-lookup"><span data-stu-id="26de9-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="26de9-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="26de9-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="26de9-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="26de9-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="26de9-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="26de9-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="26de9-132">指令碼</span><span class="sxs-lookup"><span data-stu-id="26de9-132">Script</span></span></td>
    <td><span data-ttu-id="26de9-133">TRANSACT-SQL 指令碼 toobe 跨資料庫執行時使用。</span><span class="sxs-lookup"><span data-stu-id="26de9-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="26de9-134">hello 指令碼應該撰寫的 toobe 具有等冪性，因為 hello 服務將會重試執行失敗時的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="26de9-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="26de9-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="26de9-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="26de9-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="26de9-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="26de9-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="26de9-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="26de9-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="26de9-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="26de9-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="26de9-139">DACPAC</span></span></td>
    <td><span data-ttu-id="26de9-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">資料層應用程式</a>封裝 toobe 套用於資料庫。</span><span class="sxs-lookup"><span data-stu-id="26de9-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="26de9-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="26de9-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="26de9-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="26de9-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="26de9-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="26de9-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="26de9-144">資料庫目標</span><span class="sxs-lookup"><span data-stu-id="26de9-144">Database Target</span></span></td>
    <td><span data-ttu-id="26de9-145">資料庫和伺服器名稱的指標 tooan Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="26de9-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="26de9-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="26de9-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="26de9-148">分區對應目標</span><span class="sxs-lookup"><span data-stu-id="26de9-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="26de9-149">使用 toodetermine 資訊儲存在分區對應的彈性資料庫內的資料庫目標和認證 toobe 組合。</span><span class="sxs-lookup"><span data-stu-id="26de9-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="26de9-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="26de9-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="26de9-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="26de9-153">自訂集合目標</span><span class="sxs-lookup"><span data-stu-id="26de9-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="26de9-154">已定義的資料庫 toocollectively 群組使用來執行。</span><span class="sxs-lookup"><span data-stu-id="26de9-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="26de9-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="26de9-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="26de9-157">自訂集合子目標</span><span class="sxs-lookup"><span data-stu-id="26de9-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="26de9-158">從自訂集合參考的資料庫目標。</span><span class="sxs-lookup"><span data-stu-id="26de9-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="26de9-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="26de9-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="26de9-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="26de9-161">作業</span><span class="sxs-lookup"><span data-stu-id="26de9-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="26de9-162">可以使用的 tootrigger 執行或 toofulfill 排程的作業參數的定義。</span><span class="sxs-lookup"><span data-stu-id="26de9-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="26de9-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="26de9-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="26de9-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="26de9-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="26de9-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="26de9-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="26de9-166">工作執行</span><span class="sxs-lookup"><span data-stu-id="26de9-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="26de9-167">容器的可執行的指令碼，或套用使用認證的資料庫連線失敗與 DACPAC tooa 目標工作所需 toofulfill 處理素來 tooan 執行原則。</span><span class="sxs-lookup"><span data-stu-id="26de9-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="26de9-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="26de9-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="26de9-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="26de9-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="26de9-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="26de9-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="26de9-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="26de9-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="26de9-172">工作作業執行</span><span class="sxs-lookup"><span data-stu-id="26de9-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="26de9-173">單一工作 toofulfill 工作單位。</span><span class="sxs-lookup"><span data-stu-id="26de9-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="26de9-174">如果作業工作不能 toosuccessfully 執行、 hello 產生的例外狀況訊息將會記錄和新的比對作業工作將會建立和執行素來 toohello 指定在執行原則。</span><span class="sxs-lookup"><span data-stu-id="26de9-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="26de9-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="26de9-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="26de9-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="26de9-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="26de9-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="26de9-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="26de9-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="26de9-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="26de9-179">工作執行原則</span><span class="sxs-lookup"><span data-stu-id="26de9-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="26de9-180">控制重試之間的工作執行逾時、重試限制和間隔。</span><span class="sxs-lookup"><span data-stu-id="26de9-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="26de9-181">彈性資料庫工作包括預設工作執行原則，基本上會導致無限的工作作業失敗重試，每次重試之間具有間隔的指數輪詢。</span><span class="sxs-lookup"><span data-stu-id="26de9-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="26de9-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="26de9-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="26de9-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="26de9-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="26de9-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="26de9-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="26de9-185">排程</span><span class="sxs-lookup"><span data-stu-id="26de9-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="26de9-186">時間基礎執行 tootake 位置上重複的間隔或一次的規格。</span><span class="sxs-lookup"><span data-stu-id="26de9-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="26de9-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="26de9-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="26de9-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="26de9-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="26de9-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="26de9-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="26de9-190">工作觸發程序</span><span class="sxs-lookup"><span data-stu-id="26de9-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="26de9-191">作業和排程 tootrigger 作業執行根據 toohello 排程之間的對應。</span><span class="sxs-lookup"><span data-stu-id="26de9-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="26de9-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="26de9-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="26de9-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="26de9-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="26de9-194">支援的彈性資料庫工作群組類型</span><span class="sxs-lookup"><span data-stu-id="26de9-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="26de9-195">hello 作業將整個群組的資料庫執行 TRANSACT-SQL (T-SQL) 指令碼或應用程式的 Dacpac。</span><span class="sxs-lookup"><span data-stu-id="26de9-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="26de9-196">工作執行時送出的 toobe 執行跨群組的資料庫，hello 工作 「 展開 」 hello 成子工作會在其中每個執行 hello 要求針對 hello 群組中的單一資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="26de9-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="26de9-197">您可以建立兩種群組：</span><span class="sxs-lookup"><span data-stu-id="26de9-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="26de9-198">[分區對應](sql-database-elastic-scale-shard-map-management.md)群組： hello 工作提交的 tootarget 分區對應作業時，查詢 hello 分區對應 toodetermine 其目前的分區集，並接著會建立子工作的每個分區 hello 分區對應中。</span><span class="sxs-lookup"><span data-stu-id="26de9-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="26de9-199">自訂集合群組：一組自訂定義的資料庫。</span><span class="sxs-lookup"><span data-stu-id="26de9-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="26de9-200">當作業目標的自訂集合時，它會建立子工作的每個資料庫目前 hello 自訂集合中。</span><span class="sxs-lookup"><span data-stu-id="26de9-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="26de9-201">tooset hello 彈性資料庫工作的連接</span><span class="sxs-lookup"><span data-stu-id="26de9-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="26de9-202">連線需要 toobe 設定 toohello 工作*控制資料庫*先前 toousing hello 作業 Api。</span><span class="sxs-lookup"><span data-stu-id="26de9-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="26de9-203">執行這個指令程式會觸發認證視窗 toopop 向上要求建立安裝彈性資料庫工作時 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="26de9-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="26de9-204">本主題中提供的所有範例都假設已經執行第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="26de9-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="26de9-205">開啟連接 toohello 彈性資料庫工作：</span><span class="sxs-lookup"><span data-stu-id="26de9-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="26de9-206">Hello 彈性資料庫工作中的加密的認證</span><span class="sxs-lookup"><span data-stu-id="26de9-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="26de9-207">資料庫認證可以插入到 hello 作業*控制資料庫*及其密碼加密。</span><span class="sxs-lookup"><span data-stu-id="26de9-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="26de9-208">它是必要的 toostore 認證 tooenable 作業 toobe 稍後的時間，在執行 （使用作業排程）。</span><span class="sxs-lookup"><span data-stu-id="26de9-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="26de9-209">加密可以通過 hello 安裝指令碼的過程中建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="26de9-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="26de9-210">hello 安裝指令碼建立和上傳 hello hello Azure 雲端服務的 hello 的解密憑證已儲存的加密的密碼。</span><span class="sxs-lookup"><span data-stu-id="26de9-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="26de9-211">稍後 hello Azure 雲端服務儲存 hello hello 作業內的公用金鑰*控制資料庫*而不需要 hello 憑證讓 hello PowerShell API 或 Azure 傳統入口網站介面 tooencrypt 提供的密碼在本機安裝 toobe。</span><span class="sxs-lookup"><span data-stu-id="26de9-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="26de9-212">hello 認證密碼會加密且安全的唯讀存取 tooElastic 資料庫作業物件的使用者。</span><span class="sxs-lookup"><span data-stu-id="26de9-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="26de9-213">但是，具有讀寫存取 tooElastic 資料庫工作物件 tooextract 密碼的惡意使用者可能會。</span><span class="sxs-lookup"><span data-stu-id="26de9-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="26de9-214">認證是設計的 toobe 重複用在作業執行。</span><span class="sxs-lookup"><span data-stu-id="26de9-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="26de9-215">建立連接時，會傳遞 tootarget 資料庫認證。</span><span class="sxs-lookup"><span data-stu-id="26de9-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="26de9-216">目前使用的每個認證的 hello 目標資料庫上沒有任何限制，惡意使用者無法加入資料庫目標 hello 惡意使用者的控制之下的資料庫。</span><span class="sxs-lookup"><span data-stu-id="26de9-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="26de9-217">hello 使用者之後無法啟動目標為此資料庫 toogain hello 認證密碼的工作。</span><span class="sxs-lookup"><span data-stu-id="26de9-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="26de9-218">彈性資料庫工作的安全性最佳作法包括：</span><span class="sxs-lookup"><span data-stu-id="26de9-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="26de9-219">限制的 hello Api tootrusted 個人的使用量。</span><span class="sxs-lookup"><span data-stu-id="26de9-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="26de9-220">憑證應該具有 hello 最低權限所需的 tooperform hello 作業工作。</span><span class="sxs-lookup"><span data-stu-id="26de9-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="26de9-221">如需詳細資訊，請參閱 [SQL Server 中的授權和權限](https://msdn.microsoft.com/library/bb669084.aspx) 這篇 MSDN 文章。</span><span class="sxs-lookup"><span data-stu-id="26de9-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="26de9-222">toocreate 跨資料庫的工作執行的是加密的認證</span><span class="sxs-lookup"><span data-stu-id="26de9-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="26de9-223">toocreate 加密新認證，hello [ **Get-credential cmdlet** ](https://technet.microsoft.com/library/hh849815.aspx)提示輸入使用者名稱和密碼，可傳遞 toohello [**新增 AzureSqlJobCredentialcmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential)。</span><span class="sxs-lookup"><span data-stu-id="26de9-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="26de9-224">tooupdate 認證</span><span class="sxs-lookup"><span data-stu-id="26de9-224">tooupdate credentials</span></span>
<span data-ttu-id="26de9-225">當密碼變更時，使用 hello [**組 AzureSqlJobCredential cmdlet** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential)組 hello 和**CredentialName**參數。</span><span class="sxs-lookup"><span data-stu-id="26de9-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="26de9-226">toodefine 的彈性資料庫分區對應目標</span><span class="sxs-lookup"><span data-stu-id="26de9-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="26de9-227">tooexecute 針對分區集中的所有資料庫作業 (使用建立[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md))，當做 hello 資料庫目標使用分區對應。</span><span class="sxs-lookup"><span data-stu-id="26de9-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="26de9-228">這個範例需要使用 hello 彈性資料庫用戶端程式庫建立的分區化應用程式。</span><span class="sxs-lookup"><span data-stu-id="26de9-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="26de9-229">請參閱 [開始使用彈性資料庫工具範例](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="26de9-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="26de9-230">hello 分區對應管理員資料庫必須設定為資料庫目標，則必須指定 hello 特定分區對應做為目標。</span><span class="sxs-lookup"><span data-stu-id="26de9-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="26de9-231">針對跨資料庫執行建立 T-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="26de9-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="26de9-232">在建立時執行的 T-SQL 指令碼，強烈建議 toobuild 它們 toobe[等冪](https://en.wikipedia.org/wiki/Idempotence)和彈性地防止失敗。</span><span class="sxs-lookup"><span data-stu-id="26de9-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="26de9-233">彈性資料庫工作會重試執行指令碼，每當執行發生失敗，不論 hello 失敗的 hello 分類。</span><span class="sxs-lookup"><span data-stu-id="26de9-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="26de9-234">使用 hello [**新增 AzureSqlJobContent cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate 和儲存指令碼執行，以及設定 hello **-ContentName**和**-CommandText**參數。</span><span class="sxs-lookup"><span data-stu-id="26de9-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="26de9-235">從檔案建立新的指令碼</span><span class="sxs-lookup"><span data-stu-id="26de9-235">Create a new script from a file</span></span>
<span data-ttu-id="26de9-236">如果檔案內定義 hello T-SQL 指令碼，則使用這個 tooimport hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="26de9-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="26de9-237">跨資料庫執行的 tooupdate T-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="26de9-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="26de9-238">這個 PowerShell 指令碼更新 hello 現有的指令碼的 T-SQL 命令文字。</span><span class="sxs-lookup"><span data-stu-id="26de9-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="26de9-239">下列設定變數的 tooreflect hello 預期指令碼定義 toobe 組 hello:</span><span class="sxs-lookup"><span data-stu-id="26de9-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="26de9-240">tooupdate hello 定義 tooan 現有指令碼</span><span class="sxs-lookup"><span data-stu-id="26de9-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="26de9-241">toocreate 作業 tooexecute 跨分區對應的指令碼</span><span class="sxs-lookup"><span data-stu-id="26de9-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="26de9-242">此 PowerShell 指令碼會啟動工作，以跨 Elastic Scale 分區對應中每個分區執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="26de9-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="26de9-243">下列變數 tooreflect hello 組 hello 預期指令碼和目標：</span><span class="sxs-lookup"><span data-stu-id="26de9-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="26de9-244">tooexecute 作業</span><span class="sxs-lookup"><span data-stu-id="26de9-244">tooexecute a job</span></span>
<span data-ttu-id="26de9-245">此 PowerShell 指令碼會執行現有工作：</span><span class="sxs-lookup"><span data-stu-id="26de9-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="26de9-246">更新下列執行變數 tooreflect hello 需要工作名稱 toohave hello:</span><span class="sxs-lookup"><span data-stu-id="26de9-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="26de9-247">單一作業執行 tooretrieve hello 狀態</span><span class="sxs-lookup"><span data-stu-id="26de9-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="26de9-248">使用 hello [ **Get AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution)組 hello 和**JobExecutionId**參數 tooview hello 狀態的作業執行。</span><span class="sxs-lookup"><span data-stu-id="26de9-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="26de9-249">使用 hello 相同**Get AzureSqlJobExecution** cmdlet 搭配 hello **includechildren 要求**參數 tooview hello 狀態的子工作執行，也就是 hello 每次針對每個工作在執行特定的狀態hello 作業為目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="26de9-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="26de9-250">跨多個工作執行 tooview hello 狀態</span><span class="sxs-lookup"><span data-stu-id="26de9-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="26de9-251">hello [ **Get AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljob)具有多個選擇性參數可能是使用的 toodisplay 多個工作執行，透過提供 hello 參數篩選。</span><span class="sxs-lookup"><span data-stu-id="26de9-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="26de9-252">hello 以下會示範一些 hello 的可能方法 toouse Get AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="26de9-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="26de9-253">擷取所有作用中最上層工作執行：</span><span class="sxs-lookup"><span data-stu-id="26de9-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="26de9-254">擷取所有最上層工作執行，包括非使用中工作執行：</span><span class="sxs-lookup"><span data-stu-id="26de9-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="26de9-255">擷取已提供工作執行 ID 的所有子工作執行，包括非使用中工作執行：</span><span class="sxs-lookup"><span data-stu-id="26de9-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="26de9-256">擷取使用排程/工作組合建立的所有工作執行，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="26de9-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="26de9-257">擷取以指定的分區對應為目標的所有工作，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="26de9-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="26de9-258">擷取以指定的自訂集合為目標的所有工作，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="26de9-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="26de9-259">擷取作業在特定的工作執行的工作執行 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="26de9-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="26de9-260">擷取工作作業執行詳細資料：</span><span class="sxs-lookup"><span data-stu-id="26de9-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="26de9-261">hello 下列 PowerShell 指令碼可以使用的 tooview hello 詳細資料的作業工作執行，這特別有用偵錯時執行失敗數目。</span><span class="sxs-lookup"><span data-stu-id="26de9-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="26de9-262">作業的工作執行的 tooretrieve 失敗</span><span class="sxs-lookup"><span data-stu-id="26de9-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="26de9-263">hello **JobTaskExecution 物件**包含 hello 生命週期的 hello 工作，以及訊息屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="26de9-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="26de9-264">如果作業工作執行失敗，hello 生命週期的屬性會設定太*失敗*和 hello 訊息屬性會設定 toohello 產生的例外狀況訊息和其堆疊。</span><span class="sxs-lookup"><span data-stu-id="26de9-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="26de9-265">如果作業失敗，會針對給定的作業不成功的作業工作的重要 tooview hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="26de9-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="26de9-266">工作執行 toocomplete 的 toowait</span><span class="sxs-lookup"><span data-stu-id="26de9-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="26de9-267">下列 PowerShell 指令碼的 hello 可使用的作業工作 toocomplete toowait:</span><span class="sxs-lookup"><span data-stu-id="26de9-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="26de9-268">建立自訂執行原則</span><span class="sxs-lookup"><span data-stu-id="26de9-268">Create a custom execution policy</span></span>
<span data-ttu-id="26de9-269">彈性資料庫工作支援建立自訂執行原則，可以在啟動作業時套用。</span><span class="sxs-lookup"><span data-stu-id="26de9-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="26de9-270">執行原則目前允許定義：</span><span class="sxs-lookup"><span data-stu-id="26de9-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="26de9-271">Hello 執行原則的名稱： 識別項。</span><span class="sxs-lookup"><span data-stu-id="26de9-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="26de9-272">工作逾時：彈性資料庫工作取消工作之前的總時間。</span><span class="sxs-lookup"><span data-stu-id="26de9-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="26de9-273">初始重試間隔： 間隔 toowait 第一次重試之前。</span><span class="sxs-lookup"><span data-stu-id="26de9-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="26de9-274">重試間隔 toouse 的最大重試間隔： 端點。</span><span class="sxs-lookup"><span data-stu-id="26de9-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="26de9-275">重試間隔輪詢： 係數使用係數 toocalculate hello 下一步 重試間隔。</span><span class="sxs-lookup"><span data-stu-id="26de9-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="26de9-276">hello 下列公式會使用: （初始的重試間隔） * Math.pow (（間隔輪詢係數） （數字的重試）-2)。</span><span class="sxs-lookup"><span data-stu-id="26de9-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="26de9-277">最大嘗試次數： hello 的數目上限重試嘗試 tooperform 工作內。</span><span class="sxs-lookup"><span data-stu-id="26de9-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="26de9-278">hello 預設執行原則會使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="26de9-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="26de9-279">名稱：預設執行原則</span><span class="sxs-lookup"><span data-stu-id="26de9-279">Name: Default execution policy</span></span>
* <span data-ttu-id="26de9-280">工作逾時：1 週</span><span class="sxs-lookup"><span data-stu-id="26de9-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="26de9-281">初始重試間隔：100 毫秒</span><span class="sxs-lookup"><span data-stu-id="26de9-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="26de9-282">最大重試間隔：30 分鐘</span><span class="sxs-lookup"><span data-stu-id="26de9-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="26de9-283">重試間隔係數：2</span><span class="sxs-lookup"><span data-stu-id="26de9-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="26de9-284">嘗試上限：2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="26de9-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="26de9-285">建立 hello 所需執行原則：</span><span class="sxs-lookup"><span data-stu-id="26de9-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="26de9-286">更新自訂執行原則</span><span class="sxs-lookup"><span data-stu-id="26de9-286">Update a custom execution policy</span></span>
<span data-ttu-id="26de9-287">更新所需的 hello 執行原則 tooupdate:</span><span class="sxs-lookup"><span data-stu-id="26de9-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="26de9-288">取消工作</span><span class="sxs-lookup"><span data-stu-id="26de9-288">Cancel a job</span></span>
<span data-ttu-id="26de9-289">彈性資料庫工作支援取消工作要求。</span><span class="sxs-lookup"><span data-stu-id="26de9-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="26de9-290">如果彈性資料庫工作偵測到目前正在執行工作的取消要求，它會嘗試 toostop hello 作業。</span><span class="sxs-lookup"><span data-stu-id="26de9-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="26de9-291">彈性資料庫工作有兩種不同的方式可以執行取消作業：</span><span class="sxs-lookup"><span data-stu-id="26de9-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="26de9-292">取消目前正在執行工作 5d;: 如果當工作目前正在執行時偵測取消，則將會取消嘗試 hello 目前正在執行的層面 hello 工作內。</span><span class="sxs-lookup"><span data-stu-id="26de9-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="26de9-293">例如： 嘗試取消時，目前執行的長時間執行查詢時，會有嘗試 toocancel hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="26de9-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="26de9-294">取消工作重試： hello 控制執行緒啟動工作執行前，取消偵測到的 hello 控制執行緒，如果將避免啟動 hello 工作，並宣告 hello 要求為已取消。</span><span class="sxs-lookup"><span data-stu-id="26de9-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="26de9-295">如果作業取消父工作的要求，hello 父工作和所有其子工作會採用 hello 取消要求。</span><span class="sxs-lookup"><span data-stu-id="26de9-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="26de9-296">toosubmit 取消要求，使用 hello [**停止 AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution)組 hello 和**JobExecutionId**參數。</span><span class="sxs-lookup"><span data-stu-id="26de9-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="26de9-297">toodelete 作業，以非同步方式作業歷程記錄</span><span class="sxs-lookup"><span data-stu-id="26de9-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="26de9-298">彈性資料庫工作支援非同步刪除工作。</span><span class="sxs-lookup"><span data-stu-id="26de9-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="26de9-299">作業可以標示為刪除，而且 hello 系統刪除 hello 工作和其所有的作業記錄所有作業執行都完成 hello 工作之後。</span><span class="sxs-lookup"><span data-stu-id="26de9-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="26de9-300">hello 系統不會自動取消作用中的作業執行。</span><span class="sxs-lookup"><span data-stu-id="26de9-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="26de9-301">叫用[**停止 AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel 作用中的作業執行。</span><span class="sxs-lookup"><span data-stu-id="26de9-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="26de9-302">tootrigger 作業刪除使用 hello [**移除 AzureSqlJob cmdlet** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob)組 hello 和**JobName**參數。</span><span class="sxs-lookup"><span data-stu-id="26de9-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="26de9-303">toocreate 自訂資料庫目標</span><span class="sxs-lookup"><span data-stu-id="26de9-303">toocreate a custom database target</span></span>
<span data-ttu-id="26de9-304">您可以定義自訂資料庫目標以直接執行或包含在自訂資料庫群組內。</span><span class="sxs-lookup"><span data-stu-id="26de9-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="26de9-305">例如，因為**彈性集區**是尚不直接支援使用 PowerShell Api，您可以建立自訂資料庫的目標和其中包含所有 hello 集區中的 hello 資料庫自訂資料庫收集目標。</span><span class="sxs-lookup"><span data-stu-id="26de9-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="26de9-306">設定下列變數 tooreflect hello 預期資料庫資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="26de9-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="26de9-307">toocreate 自訂資料庫收集目標</span><span class="sxs-lookup"><span data-stu-id="26de9-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="26de9-308">使用 hello [**新增 AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine 跨多個定義的資料庫目標的自訂資料庫集合目標 tooenable 執行。</span><span class="sxs-lookup"><span data-stu-id="26de9-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="26de9-309">在建立資料庫群組之後，資料庫可以是聯 hello 自訂集合目標。</span><span class="sxs-lookup"><span data-stu-id="26de9-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="26de9-310">設定下列變數 tooreflect hello 所需的自訂集合目標組態 hello:</span><span class="sxs-lookup"><span data-stu-id="26de9-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="26de9-311">tooadd 資料庫 tooa 自訂資料庫收集目標</span><span class="sxs-lookup"><span data-stu-id="26de9-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="26de9-312">tooadd 資料庫 tooa 特定自訂集合使用 hello [**新增 AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="26de9-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="26de9-313">檢閱 hello 資料庫內的自訂資料庫收集目標</span><span class="sxs-lookup"><span data-stu-id="26de9-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="26de9-314">使用 hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello 子資料庫內的自訂資料庫收集目標。</span><span class="sxs-lookup"><span data-stu-id="26de9-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="26de9-315">建立指令碼工作 tooexecute 跨自訂資料庫收集目標</span><span class="sxs-lookup"><span data-stu-id="26de9-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="26de9-316">使用 hello [**新增 AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate 作業會每天針對資料庫定義的自訂資料庫收集目標的群組。</span><span class="sxs-lookup"><span data-stu-id="26de9-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="26de9-317">彈性資料庫工作會展開成多個子工作，每個對應的 tooa 資料庫與 hello 自訂資料庫收集目標關聯，並確保 hello 指令碼執行的每個資料庫的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="26de9-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="26de9-318">同樣地，請務必指令碼是等冪 toobe 彈性 tooretries。</span><span class="sxs-lookup"><span data-stu-id="26de9-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="26de9-319">跨資料庫的資料集合</span><span class="sxs-lookup"><span data-stu-id="26de9-319">Data collection across databases</span></span>
<span data-ttu-id="26de9-320">您可以使用作業 tooexecute 查詢整個群組的資料庫，並傳送 hello 結果 tooa 特定資料表。</span><span class="sxs-lookup"><span data-stu-id="26de9-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="26de9-321">hello 資料表可以查詢之後每個資料庫的 hello 事實 toosee hello 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="26de9-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="26de9-322">這樣非同步方法 tooexecute 查詢跨多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="26de9-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="26de9-323">嘗試失敗時自動經由重試來處理。</span><span class="sxs-lookup"><span data-stu-id="26de9-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="26de9-324">如果它尚未存在，就會自動建立 hello 指定的目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="26de9-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="26de9-325">hello 新的資料表符合傳回的結果集的 hello hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="26de9-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="26de9-326">如果指令碼傳回多個結果集，彈性資料庫工作才會傳送 hello 第一個 toohello 目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="26de9-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="26de9-327">hello 下列 PowerShell 指令碼執行指令碼，並會將其結果收集到指定的資料表。</span><span class="sxs-lookup"><span data-stu-id="26de9-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="26de9-328">此指令碼假設已建立一個會輸出單一結果集的 T-SQL 指令碼，也假設已建立自訂資料庫集合目標。</span><span class="sxs-lookup"><span data-stu-id="26de9-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="26de9-329">此指令碼使用 hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="26de9-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="26de9-330">設定指令碼、 認證和執行目標的 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="26de9-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="26de9-331">toocreate 與開始的工作資料收集案例。</span><span class="sxs-lookup"><span data-stu-id="26de9-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="26de9-332">此指令碼使用 hello [**開始 AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="26de9-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="26de9-333">tooschedule 工作執行觸發程序</span><span class="sxs-lookup"><span data-stu-id="26de9-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="26de9-334">hello 下列 PowerShell 指令碼可以使用的 toocreate 週期性的排程。</span><span class="sxs-lookup"><span data-stu-id="26de9-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="26de9-335">這個指令碼使用分鐘間隔，但是 [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) 也支援 -DayInterval、-HourInterval、-MonthInterval 和 -WeekInterval 參數。</span><span class="sxs-lookup"><span data-stu-id="26de9-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="26de9-336">您可以藉由傳遞 -OneTime，建立僅執行一次的排程。</span><span class="sxs-lookup"><span data-stu-id="26de9-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="26de9-337">建立新的排程：</span><span class="sxs-lookup"><span data-stu-id="26de9-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="26de9-338">tootrigger 的時間排程執行的工作</span><span class="sxs-lookup"><span data-stu-id="26de9-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="26de9-339">工作觸發程序可以定義的 toohave 作業執行相應 tooa 時間排程。</span><span class="sxs-lookup"><span data-stu-id="26de9-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="26de9-340">hello 下列 PowerShell 指令碼可以使用的 toocreate 工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="26de9-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="26de9-341">使用[新增 AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger)組 hello 遵循變數 toocorrespond toohello 所需的作業和排程：</span><span class="sxs-lookup"><span data-stu-id="26de9-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="26de9-342">tooremove 排程的關聯 toostop 作業依排程執行</span><span class="sxs-lookup"><span data-stu-id="26de9-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="26de9-343">可以移除 toodiscontinue 再度工作執行的工作觸發程序，hello 工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="26de9-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="26de9-344">移除工作觸發程序 toostop 工作正在執行使用 hello 相應 tooa 排程[**移除 AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger)。</span><span class="sxs-lookup"><span data-stu-id="26de9-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="26de9-345">擷取工作觸發程序繫結的 tooa 次的排程</span><span class="sxs-lookup"><span data-stu-id="26de9-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="26de9-346">hello 下列 PowerShell 指令碼可以使用的 tooobtain 和顯示 hello 工作觸發程序的已註冊的 tooa 特定時間排程。</span><span class="sxs-lookup"><span data-stu-id="26de9-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="26de9-347">tooretrieve 工作觸發程序繫結的 tooa 工作</span><span class="sxs-lookup"><span data-stu-id="26de9-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="26de9-348">使用[Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain 並顯示包含已註冊的工作的排程。</span><span class="sxs-lookup"><span data-stu-id="26de9-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="26de9-349">toocreate 執行跨資料庫的資料層應用程式 (DACPAC)</span><span class="sxs-lookup"><span data-stu-id="26de9-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="26de9-350">toocreate DACPAC，請參閱[資料層應用程式](https://msdn.microsoft.com/library/ee210546.aspx)。</span><span class="sxs-lookup"><span data-stu-id="26de9-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="26de9-351">toodeploy DACPAC 中，使用 hello[新增 AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent)。</span><span class="sxs-lookup"><span data-stu-id="26de9-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="26de9-352">hello DACPAC 必須是可存取 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="26de9-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="26de9-353">它會建議 tooupload 建立的 DACPAC tooAzure 儲存體，並建立[共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md)hello DACPAC。</span><span class="sxs-lookup"><span data-stu-id="26de9-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="26de9-354">tooupdate 執行跨資料庫的資料層應用程式 (DACPAC)</span><span class="sxs-lookup"><span data-stu-id="26de9-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="26de9-355">彈性資料庫工作中註冊的現有 Dacpac 可以更新的 toopoint toonew Uri。</span><span class="sxs-lookup"><span data-stu-id="26de9-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="26de9-356">使用 hello [**組 AzureSqlJobContentDefinition cmdlet** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI 上的現有已註冊的 DACPAC:</span><span class="sxs-lookup"><span data-stu-id="26de9-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="26de9-357">toocreate 作業 tooapply 跨資料庫的資料層應用程式 (DACPAC)</span><span class="sxs-lookup"><span data-stu-id="26de9-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="26de9-358">DACPAC 彈性資料庫工作內建立之後，可以建立工作 tooapply hello DACPAC 跨資料庫的群組。</span><span class="sxs-lookup"><span data-stu-id="26de9-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="26de9-359">下列 PowerShell 指令碼的 hello 可在自訂集合的資料庫之間使用的 toocreate DACPAC 作業：</span><span class="sxs-lookup"><span data-stu-id="26de9-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
