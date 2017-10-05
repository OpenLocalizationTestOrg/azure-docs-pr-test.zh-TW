---
title: "使用 PowerShell 建立和管理彈性作業 | Microsoft Docs"
description: "用來管理 Azure SQL Database 集區的 PowerShell"
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
ms.openlocfilehash: b4c97e8f51581f9a3f7c5a8d8e82562255fe7b48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="5b1ab-103">使用 PowerShell 建立和管理 SQL Database 彈性作業 (預覽)</span><span class="sxs-lookup"><span data-stu-id="5b1ab-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="5b1ab-104">適用於 **彈性資料庫工作** (預覽版) 的 PowerShell API 可讓您定義一組資料庫，然後針對這組資料庫執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="5b1ab-105">本文將說明如何使用 Powershell Cmdlet 建立和管理 **彈性資料庫工作** 。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="5b1ab-106">請參閱 [彈性工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5b1ab-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="5b1ab-107">Prerequisites</span></span>
* <span data-ttu-id="5b1ab-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-108">An Azure subscription.</span></span> <span data-ttu-id="5b1ab-109">如需免費試用，請參閱 [免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5b1ab-110">一組使用彈性資料庫工具所建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="5b1ab-111">請參閱 [開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="5b1ab-112">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-112">Azure PowerShell.</span></span> <span data-ttu-id="5b1ab-113">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-113">For detailed information, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="5b1ab-114">**彈性資料庫工作** PowerShell 封裝：請參閱 [安裝彈性資料庫工作](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="5b1ab-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="5b1ab-115">選取您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5b1ab-115">Select your Azure subscription</span></span>
<span data-ttu-id="5b1ab-116">若要選取所需的訂用帳戶，您必須提供訂用帳戶 ID (**-SubscriptionId**) 或訂用帳戶名稱 (**-SubscriptionName**)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="5b1ab-117">如果您有多個訂用帳戶，則可以執行 **Get-AzureRmSubscription** Cmdlet，然後從結果集複製所需的訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="5b1ab-118">一旦您具有訂用帳戶資訊，請執行下列 commandlet 將此訂用帳戶設定為預設值，也就是建立和管理工作的目標：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="5b1ab-119">建議使用 [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) 以針對彈性資料庫工作開發和執行 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="5b1ab-120">彈性資料庫工作物件</span><span class="sxs-lookup"><span data-stu-id="5b1ab-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="5b1ab-121">下表列出 **彈性資料庫工作** 的所有物件類型，以及其描述和相關 PowerShell API。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="5b1ab-122">物件類型</span><span class="sxs-lookup"><span data-stu-id="5b1ab-122">Object Type</span></span></th>
    <th><span data-ttu-id="5b1ab-123">說明</span><span class="sxs-lookup"><span data-stu-id="5b1ab-123">Description</span></span></th>
    <th><span data-ttu-id="5b1ab-124">相關 PowerShell API</span><span class="sxs-lookup"><span data-stu-id="5b1ab-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="5b1ab-125">認證</span><span class="sxs-lookup"><span data-stu-id="5b1ab-125">Credential</span></span></td>
    <td><span data-ttu-id="5b1ab-126">連接到資料庫以執行指令碼或 DACPAC 的應用程式時使用的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="5b1ab-127">密碼在傳送並儲存在彈性資料庫工作資料庫之前會先行加密。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="5b1ab-128">密碼會由彈性資料庫工作服務透過安裝指令碼建立及上傳的認證解密。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="5b1ab-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="5b1ab-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="5b1ab-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="5b1ab-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="5b1ab-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="5b1ab-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="5b1ab-132">指令碼</span><span class="sxs-lookup"><span data-stu-id="5b1ab-132">Script</span></span></td>
    <td><span data-ttu-id="5b1ab-133">用於跨資料庫執行的 Transact-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="5b1ab-134">指令碼應該撰寫為等冪，因為服務將會在失敗時重試執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="5b1ab-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="5b1ab-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="5b1ab-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="5b1ab-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="5b1ab-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="5b1ab-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="5b1ab-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="5b1ab-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="5b1ab-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="5b1ab-139">DACPAC</span></span></td>
    <td><span data-ttu-id="5b1ab-140">要跨資料庫套用的<a href="https://msdn.microsoft.com/library/ee210546.aspx">資料層應用程式</a>套件。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="5b1ab-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="5b1ab-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="5b1ab-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="5b1ab-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="5b1ab-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="5b1ab-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="5b1ab-144">資料庫目標</span><span class="sxs-lookup"><span data-stu-id="5b1ab-144">Database Target</span></span></td>
    <td><span data-ttu-id="5b1ab-145">指向 Azure SQL Database 的資料庫和伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="5b1ab-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="5b1ab-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="5b1ab-148">分區對應目標</span><span class="sxs-lookup"><span data-stu-id="5b1ab-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="5b1ab-149">資料庫目標和認證的組合，用來判斷彈性資料庫分區對應內儲存的資訊。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="5b1ab-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="5b1ab-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="5b1ab-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="5b1ab-153">自訂集合目標</span><span class="sxs-lookup"><span data-stu-id="5b1ab-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="5b1ab-154">共同用於執行的已定義資料庫群組。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="5b1ab-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="5b1ab-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="5b1ab-157">自訂集合子目標</span><span class="sxs-lookup"><span data-stu-id="5b1ab-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="5b1ab-158">從自訂集合參考的資料庫目標。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="5b1ab-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="5b1ab-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="5b1ab-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="5b1ab-161">工作 (Job)</span><span class="sxs-lookup"><span data-stu-id="5b1ab-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="5b1ab-162">工作的參數的定義，可用來觸發執行或完成排程。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="5b1ab-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="5b1ab-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="5b1ab-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="5b1ab-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="5b1ab-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="5b1ab-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="5b1ab-166">工作執行</span><span class="sxs-lookup"><span data-stu-id="5b1ab-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="5b1ab-167">必要的作業容器，以使用資料庫連線的認證執行指令碼或將 DACPAC 套用到目標，具有根據執行原則處理的失敗。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="5b1ab-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="5b1ab-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="5b1ab-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="5b1ab-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="5b1ab-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="5b1ab-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="5b1ab-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="5b1ab-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="5b1ab-172">工作作業執行</span><span class="sxs-lookup"><span data-stu-id="5b1ab-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="5b1ab-173">完成作業的單一工作單位。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="5b1ab-174">如果工作作業不能成功執行，將會記錄產生的例外狀況訊息，並且建立新的比對工作作業及根據指定的執行原則執行。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="5b1ab-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="5b1ab-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="5b1ab-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="5b1ab-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="5b1ab-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="5b1ab-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="5b1ab-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="5b1ab-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="5b1ab-179">工作執行原則</span><span class="sxs-lookup"><span data-stu-id="5b1ab-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="5b1ab-180">控制重試之間的工作執行逾時、重試限制和間隔。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="5b1ab-181">彈性資料庫工作包括預設工作執行原則，基本上會導致無限的工作作業失敗重試，每次重試之間具有間隔的指數輪詢。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="5b1ab-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="5b1ab-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="5b1ab-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="5b1ab-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="5b1ab-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="5b1ab-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="5b1ab-185">排程</span><span class="sxs-lookup"><span data-stu-id="5b1ab-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="5b1ab-186">以時間為基礎的執行指定會在重複間隔發生或單一次數發生。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="5b1ab-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="5b1ab-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="5b1ab-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="5b1ab-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="5b1ab-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="5b1ab-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="5b1ab-190">工作觸發程序</span><span class="sxs-lookup"><span data-stu-id="5b1ab-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="5b1ab-191">工作與排程之間的對應，以根據排程觸發工作執行。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="5b1ab-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="5b1ab-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="5b1ab-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="5b1ab-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="5b1ab-194">支援的彈性資料庫工作群組類型</span><span class="sxs-lookup"><span data-stu-id="5b1ab-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="5b1ab-195">工作可以跨資料庫群組執行 Transact-SQL (T-SQL) 指令碼或 DACPAC 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="5b1ab-196">將提交工作是跨資料庫群組執行時，工作會「展開」子工作，由每個子工作針對群組中的單一資料庫執行要求的動作。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="5b1ab-197">您可以建立兩種群組：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="5b1ab-198">[分區對應](sql-database-elastic-scale-shard-map-management.md) 群組：當提交工作是以分區對應為目標時，工作會先查詢分區對應來判斷其目前的分區集，然後為分區對應中的每個分區建立子工作。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="5b1ab-199">自訂集合群組：一組自訂定義的資料庫。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="5b1ab-200">當工作以自訂集合為目標時，它會為目前在自訂集合中的每個資料庫建立子工作。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="5b1ab-201">設定彈性資料庫工作連接</span><span class="sxs-lookup"><span data-stu-id="5b1ab-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="5b1ab-202">使用工作 API 之前，必須設定工作「控制資料庫」  的連接。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="5b1ab-203">執行此 Cmdlet 會顯示認證視窗，要求提供安裝彈性資料庫工作時所建立的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="5b1ab-204">本主題中提供的所有範例都假設已經執行第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="5b1ab-205">開啟彈性資料庫工作的連線：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="5b1ab-206">彈性資料庫工作內的已加密認證</span><span class="sxs-lookup"><span data-stu-id="5b1ab-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="5b1ab-207">資料庫認證可以插入至工作的「控制資料庫」，而且密碼會加密。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="5b1ab-208">必須儲存認證，稍後才能執行工作 (使用工作排程)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="5b1ab-209">加密是透過建立為安裝指令碼一部分的憑證來運作。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="5b1ab-210">安裝指令碼會建立憑證並將其上傳至 Azure 雲端服務，以解密已儲存的加密密碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="5b1ab-211">Azure 雲端服務稍後會在工作的「控制資料庫」  內儲存公開金鑰，讓 PowerShell API 或 Azure 傳統入口網站介面加密提供的密碼，而不需要在本機安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="5b1ab-212">認證密碼會加密，以防範對彈性資料庫工作物件只具有唯讀存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="5b1ab-213">但對於彈性資料庫工作物件具有讀寫存取權的惡意使用者，有可能會擷取密碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="5b1ab-214">認證是設計為跨工作執行重複使用。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="5b1ab-215">當建立連線時，認證會傳遞至目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="5b1ab-216">用於每個認證的目標資料庫目前沒有限制，惡意使用者可以為他掌控之下的資料庫加入資料庫目標。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="5b1ab-217">該使用者接著就可以針對此資料庫啟動工作，取得認證的密碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="5b1ab-218">彈性資料庫工作的安全性最佳作法包括：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="5b1ab-219">將 API 的使用限制為受信任的個人。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="5b1ab-220">認證應該具有執行工作作業所需的最低權限。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="5b1ab-221">如需詳細資訊，請參閱 [SQL Server 中的授權和權限](https://msdn.microsoft.com/library/bb669084.aspx) 這篇 MSDN 文章。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="5b1ab-222">建立跨資料庫執行工作的加密認證</span><span class="sxs-lookup"><span data-stu-id="5b1ab-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="5b1ab-223">若要建立新的加密認證，[**Get-Credential Cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) 會提示您輸入可以傳遞至 [**New-AzureSqlJobCredential Cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential) 的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="5b1ab-224">更新認證</span><span class="sxs-lookup"><span data-stu-id="5b1ab-224">To update credentials</span></span>
<span data-ttu-id="5b1ab-225">當密碼變更時，請使用 [**Set-AzureSqlJobCredential Cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) 並設定 **CredentialName** 參數。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="5b1ab-226">定義彈性資料庫分區對應目標</span><span class="sxs-lookup"><span data-stu-id="5b1ab-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="5b1ab-227">若要針對分區集的所有資料庫執行作業 (使用 [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)建立)，請使用分區對應做為資料庫目標。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="5b1ab-228">此範例需要一個使用彈性資料庫用戶端程式庫建立的分區應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="5b1ab-229">請參閱 [開始使用彈性資料庫工具範例](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="5b1ab-230">您必須將分區對應管理員資料庫設為資料庫目標，然後將特定分區對應指定為目標。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="5b1ab-231">針對跨資料庫執行建立 T-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="5b1ab-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="5b1ab-232">建立要執行的 T-SQL 指令碼時，強烈建議將其建置為 [等冪性質](https://en.wikipedia.org/wiki/Idempotence) 且失敗時迅速恢復。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="5b1ab-233">每當執行發生失敗時，不論失敗的分類，彈性資料庫工作將重試執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="5b1ab-234">使用 [**New-AzureSqlJobContent Cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) 建立並儲存要執行的指令碼，並且設定 **-ContentName** 和 **-CommandText** 參數。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-234">Use the [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="5b1ab-235">從檔案建立新的指令碼</span><span class="sxs-lookup"><span data-stu-id="5b1ab-235">Create a new script from a file</span></span>
<span data-ttu-id="5b1ab-236">如果 T-SQL 指令碼定義在檔案內，請利用此選項匯入指令碼：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="5b1ab-237">針對跨資料庫執行更新 T-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="5b1ab-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="5b1ab-238">此 PowerShell 指令碼會更新現有指令碼的 T-SQL 命令文字。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="5b1ab-239">設定下列變數以反映要設定的所需指令碼定義：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
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

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="5b1ab-240">更新現有指令碼的定義</span><span class="sxs-lookup"><span data-stu-id="5b1ab-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="5b1ab-241">建立工作以跨分區對應執行指令碼</span><span class="sxs-lookup"><span data-stu-id="5b1ab-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="5b1ab-242">此 PowerShell 指令碼會啟動工作，以跨 Elastic Scale 分區對應中每個分區執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="5b1ab-243">設定下列變數以反映所需的指令碼和目標：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="5b1ab-244">執行工作</span><span class="sxs-lookup"><span data-stu-id="5b1ab-244">To execute a job</span></span>
<span data-ttu-id="5b1ab-245">此 PowerShell 指令碼會執行現有工作：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="5b1ab-246">更新下列變數以反映要執行的所需工作名稱：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="5b1ab-247">擷取單一工作執行的狀態</span><span class="sxs-lookup"><span data-stu-id="5b1ab-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="5b1ab-248">使用 [**Get-AzureSqlJobExecution Cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) 並且設定 **JobExecutionId** 參數，以檢視工作執行的狀態。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-248">Use the [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="5b1ab-249">使用相同 **Get-AzureSqlJobExecution** Cmdlet 搭配 **IncludeChildren** 參數，以檢視子工作執行的狀態，也就是工作在每個目標資料庫上的每個工作執行的特定狀態。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="5b1ab-250">檢視跨多個工作執行的狀態</span><span class="sxs-lookup"><span data-stu-id="5b1ab-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="5b1ab-251">[**Get-AzureSqlJobExecution Cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) 具有多個選用參數，可用來顯示多個工作執行、透過提供的參數篩選。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-251">The [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="5b1ab-252">以下示範一些使用 Get-AzureSqlJobExecution 的可能方式：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="5b1ab-253">擷取所有作用中最上層工作執行：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="5b1ab-254">擷取所有最上層工作執行，包括非使用中工作執行：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="5b1ab-255">擷取已提供工作執行 ID 的所有子工作執行，包括非使用中工作執行：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="5b1ab-256">擷取使用排程/工作組合建立的所有工作執行，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="5b1ab-257">擷取以指定的分區對應為目標的所有工作，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="5b1ab-258">擷取以指定的自訂集合為目標的所有工作，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="5b1ab-259">擷取特定工作執行內的工作作業執行的清單：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="5b1ab-260">擷取工作作業執行詳細資料：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="5b1ab-261">下列 PowerShell 指令碼可用來檢視工作作業執行的詳細資料，在偵錯執行失敗時特別有用。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="5b1ab-262">擷取工作作業執行內的失敗</span><span class="sxs-lookup"><span data-stu-id="5b1ab-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="5b1ab-263">**JobTaskExecution 物件** 包括作業生命週期的屬性和訊息屬性。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="5b1ab-264">如果工作作業執行失敗，生命週期屬性將設為「失敗」  ，且訊息屬性將設為產生的例外狀況訊息和其堆疊。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="5b1ab-265">如果工作不成功，務必檢視指定作業不成功的工作作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="5b1ab-266">等候工作執行完成</span><span class="sxs-lookup"><span data-stu-id="5b1ab-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="5b1ab-267">下列 PowerShell 指令碼可以用來等候工作作業完成：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="5b1ab-268">建立自訂執行原則</span><span class="sxs-lookup"><span data-stu-id="5b1ab-268">Create a custom execution policy</span></span>
<span data-ttu-id="5b1ab-269">彈性資料庫工作支援建立自訂執行原則，可以在啟動作業時套用。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="5b1ab-270">執行原則目前允許定義：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="5b1ab-271">名稱：執行原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="5b1ab-272">工作逾時：彈性資料庫工作取消工作之前的總時間。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="5b1ab-273">初始重試間隔：第一次重試之前等候的間隔。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="5b1ab-274">最大重試間隔：要使用的重試間隔端點。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="5b1ab-275">重試間隔輪詢係數：用來計算重試之間下一個間隔的係數。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="5b1ab-276">使用下列公式：(初始重試間隔) * Math.pow ((間隔輪詢係數), (重試次數) -2)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-276">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="5b1ab-277">嘗試上限：工作內執行的重試嘗試數目上限。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="5b1ab-278">預設的執行原則會使用下列值：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="5b1ab-279">名稱：預設執行原則</span><span class="sxs-lookup"><span data-stu-id="5b1ab-279">Name: Default execution policy</span></span>
* <span data-ttu-id="5b1ab-280">工作逾時：1 週</span><span class="sxs-lookup"><span data-stu-id="5b1ab-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="5b1ab-281">初始重試間隔：100 毫秒</span><span class="sxs-lookup"><span data-stu-id="5b1ab-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="5b1ab-282">最大重試間隔：30 分鐘</span><span class="sxs-lookup"><span data-stu-id="5b1ab-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="5b1ab-283">重試間隔係數：2</span><span class="sxs-lookup"><span data-stu-id="5b1ab-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="5b1ab-284">嘗試上限：2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="5b1ab-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="5b1ab-285">建立想要的執行原則：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="5b1ab-286">更新自訂執行原則</span><span class="sxs-lookup"><span data-stu-id="5b1ab-286">Update a custom execution policy</span></span>
<span data-ttu-id="5b1ab-287">更新要更新之想要的執行原則：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="5b1ab-288">取消工作</span><span class="sxs-lookup"><span data-stu-id="5b1ab-288">Cancel a job</span></span>
<span data-ttu-id="5b1ab-289">彈性資料庫工作支援取消工作要求。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="5b1ab-290">如果彈性資料庫工作偵測到目前正在執行工作的取消要求，它會嘗試停止工作。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="5b1ab-291">彈性資料庫工作有兩種不同的方式可以執行取消作業：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="5b1ab-292">取消目前正在執行的作業：如果作業正在執行時偵測到取消，將會在目前正在執行的作業層面內嘗試取消。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="5b1ab-293">例如：當嘗試取消時，如果有長時間執行查詢目前正在執行，將會嘗試取消查詢。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="5b1ab-294">取消作業重試：如果控制執行緒在啟動作業執行之前偵測到取消，控制執行緒會避免啟動作業，並且將要求宣告為已取消。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="5b1ab-295">如果針對父工作要求工作取消，則會對父工作和其所有子工作執行取消要求。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="5b1ab-296">若要提交取消要求，請使用 [**Stop-AzureSqlJobExecution Cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) 並設定 **JobExecutionId** 參數。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="5b1ab-297">以非同步方式刪除工作和工作歷程記錄</span><span class="sxs-lookup"><span data-stu-id="5b1ab-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="5b1ab-298">彈性資料庫工作支援非同步刪除工作。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="5b1ab-299">工作可以標示為刪除，系統將會在工作的工作執行皆已完成之後，刪除工作和其所有工作歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="5b1ab-300">系統不會自動取消作用中的工作執行。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="5b1ab-301">叫用 [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) 以取消作用中的工作執行。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) to cancel active job executions.</span></span>

<span data-ttu-id="5b1ab-302">若要觸發工作刪除，請使用 [**Remove-AzureSqlJob Cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) 並設定 **JobName** 參數。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="5b1ab-303">建立自訂資料庫目標</span><span class="sxs-lookup"><span data-stu-id="5b1ab-303">To create a custom database target</span></span>
<span data-ttu-id="5b1ab-304">您可以定義自訂資料庫目標以直接執行或包含在自訂資料庫群組內。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="5b1ab-305">例如，由於使用 PowerShell API 還無法直接支援「彈性集區」，因此您可以建立自訂資料庫目標和自訂資料庫集合目標，以包含集區中的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="5b1ab-306">設定下列變數以反映所需的資料庫資訊：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="5b1ab-307">建立自訂資料庫集合目標</span><span class="sxs-lookup"><span data-stu-id="5b1ab-307">To create a custom database collection target</span></span>
<span data-ttu-id="5b1ab-308">使用 [**New-AzureSqlJobTarget Cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) 定義自訂資料庫集合目標，以跨多個已定義的資料庫目標執行。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-308">Use the [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="5b1ab-309">建立資料庫群組之後，資料庫可以與自訂集合目標相關聯。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="5b1ab-310">設定下列變數以反映所需的自訂集合目標組態：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="5b1ab-311">將資料庫新增至自訂資料庫集合目標</span><span class="sxs-lookup"><span data-stu-id="5b1ab-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="5b1ab-312">若要將資料庫新增至特定的自訂集合，請使用 [**Add-AzureSqlJobChildTarget Cmdlet**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="5b1ab-313">檢閱自訂資料庫集合目標內的資料庫</span><span class="sxs-lookup"><span data-stu-id="5b1ab-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="5b1ab-314">使用 [**Get-AzureSqlJobTarget Cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) 以擷取自訂資料庫集合目標內的子資料庫。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-314">Use the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="5b1ab-315">建立工作以跨自訂資料庫集合目標執行指令碼</span><span class="sxs-lookup"><span data-stu-id="5b1ab-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="5b1ab-316">使用 [**New-AzureSqlJob Cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) 以根據自訂資料庫集合目標定義的資料庫群組建立工作。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-316">Use the [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="5b1ab-317">彈性資料庫工作會將工作展開成多個子工作，每個子工作對應至與自訂資料庫集合目標相關聯的資料庫，並且確保指令碼會針對每個資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="5b1ab-318">再次重申，很重要的是指令碼具有等冪處理重試的彈性。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="5b1ab-319">跨資料庫的資料集合</span><span class="sxs-lookup"><span data-stu-id="5b1ab-319">Data collection across databases</span></span>
<span data-ttu-id="5b1ab-320">您可以使用工作來跨一組資料庫執行查詢，並將結果傳送至特定的資料表。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="5b1ab-321">可以在事實之後查詢資料表，以查看每個資料庫的查詢結果。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="5b1ab-322">這麼做即可以非同步方式執行跨許多資料庫的查詢。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="5b1ab-323">嘗試失敗時自動經由重試來處理。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="5b1ab-324">如果指定的目的地資料表尚未存在，則會自動建立。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="5b1ab-325">新的資料表符合傳回的結果集的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="5b1ab-326">如果指令碼傳回多個結果集，彈性資料庫工作只會將第一個結果集傳送至目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="5b1ab-327">下列 PowerShell 指令碼會執行指令碼，並將結果收集至指定的資料表。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="5b1ab-328">此指令碼假設已建立一個會輸出單一結果集的 T-SQL 指令碼，也假設已建立自訂資料庫集合目標。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="5b1ab-329">此指令碼使用 [**Get-AzureSqlJobTarget Cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-329">This script uses the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="5b1ab-330">設定指令碼、認證和執行目標的參數：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="5b1ab-331">建立和啟動資料庫集合案例的工作</span><span class="sxs-lookup"><span data-stu-id="5b1ab-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="5b1ab-332">此指令碼使用 [**Start-AzureSqlJobExecution Cmdlet**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-332">This script uses the [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="5b1ab-333">排程工作執行觸發程序</span><span class="sxs-lookup"><span data-stu-id="5b1ab-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="5b1ab-334">下列 PowerShell 指令碼可以用來建立週期性排程。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="5b1ab-335">這個指令碼使用分鐘間隔，但是 [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) 也支援 -DayInterval、-HourInterval、-MonthInterval 和 -WeekInterval 參數。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="5b1ab-336">您可以藉由傳遞 -OneTime，建立僅執行一次的排程。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="5b1ab-337">建立新的排程：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="5b1ab-338">觸發依時間排程執行的工作</span><span class="sxs-lookup"><span data-stu-id="5b1ab-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="5b1ab-339">可以定義工作觸發程序，讓工作根據時間排程執行。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="5b1ab-340">下列 PowerShell 指令碼可以用來建立工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="5b1ab-341">使用 [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) ，並設定下列變數以對應至所需的工作和排程：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="5b1ab-342">移除排程關聯以停止依排程執行工作</span><span class="sxs-lookup"><span data-stu-id="5b1ab-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="5b1ab-343">若要透過工作觸發程序中止工作重複執行，可以移除工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="5b1ab-344">使用 [**Remove-AzureSqlJobTrigger Cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger)，移除工作觸發程序以停止工作根據排程執行。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="5b1ab-345">擷取繫結至時間排程的工作觸發程序</span><span class="sxs-lookup"><span data-stu-id="5b1ab-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="5b1ab-346">下列 PowerShell 指令碼可用來取得並顯示註冊至特定時間排程的工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="5b1ab-347">擷取繫結至工作的工作觸發程序</span><span class="sxs-lookup"><span data-stu-id="5b1ab-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="5b1ab-348">使用 [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) 以取得和顯示包含已註冊工作的排程。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="5b1ab-349">建立資料層應用程式 (DACPAC) 以跨資料庫執行</span><span class="sxs-lookup"><span data-stu-id="5b1ab-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="5b1ab-350">若要建立 DACPAC，請參閱 [資料層應用程式](https://msdn.microsoft.com/library/ee210546.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="5b1ab-351">若要部署 DACPAC、請使用 [New-AzureSqlJobContent Cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent)。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="5b1ab-352">DACPAC 必須可供服務存取。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="5b1ab-353">建議將建立的 DACPAC 上傳至 Azure 儲存體，並且為 DACPAC 建立 [共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="5b1ab-354">更新資料層應用程式 (DACPAC) 以跨資料庫執行</span><span class="sxs-lookup"><span data-stu-id="5b1ab-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="5b1ab-355">彈性資料庫工作內的現有已註冊 DACPAC 可以更新以指向新的 URI。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="5b1ab-356">使用 [**Set-AzureSqlJobContentDefinition Cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) 更新現有已註冊 DACPAC 上的 DACPAC URI：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="5b1ab-357">建立工作以跨資料庫套用資料層應用程式 (DACPAC)</span><span class="sxs-lookup"><span data-stu-id="5b1ab-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="5b1ab-358">在彈性資料庫工作內建立 DACPAC 之後，可以建立工作以跨資料庫群組套用 DACPAC。</span><span class="sxs-lookup"><span data-stu-id="5b1ab-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="5b1ab-359">下列 PowerShell 指令碼可以用來跨自訂資料庫集合建立 DACPAC 工作：</span><span class="sxs-lookup"><span data-stu-id="5b1ab-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

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
