---
title: "Azure 批次中的使用者帳戶下 aaaRun 工作 |Microsoft 文件"
description: "設定在 Azure Batch 中執行工作所需的使用者帳戶"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="a57fa-103">在 Batch 中的使用者帳戶執行工作</span><span class="sxs-lookup"><span data-stu-id="a57fa-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="a57fa-104">Azure Batch 中的工作一律會在使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="a57fa-105">根據預設，會在標準使用者帳戶中執行工作，而不需要系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="a57fa-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="a57fa-106">這些預設使用者帳戶設定通常已足夠。</span><span class="sxs-lookup"><span data-stu-id="a57fa-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="a57fa-107">某些情況下，不過，對於您想要在其下工作 toorun 有用 toobe 無法 tooconfigure hello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="a57fa-108">這篇文章討論 hello 類型的使用者帳戶以及如何設定這些案例。</span><span class="sxs-lookup"><span data-stu-id="a57fa-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="a57fa-109">使用者帳戶的類型</span><span class="sxs-lookup"><span data-stu-id="a57fa-109">Types of user accounts</span></span>

<span data-ttu-id="a57fa-110">Azure Batch 提供執行工作所需的兩種使用者帳戶類型︰</span><span class="sxs-lookup"><span data-stu-id="a57fa-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="a57fa-111">**自動使用者帳戶。**</span><span class="sxs-lookup"><span data-stu-id="a57fa-111">**Auto-user accounts.**</span></span> <span data-ttu-id="a57fa-112">自動使用者帳戶是 hello 批次服務會自動建立的內建的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="a57fa-113">根據預設，工作會在自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="a57fa-114">您可以設定的自動使用者帳戶工作執行工作 tooindicate hello 自動使用者規格。</span><span class="sxs-lookup"><span data-stu-id="a57fa-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="a57fa-115">hello 自動使用者規格可讓您 toospecify hello 提高權限層級和領域的 hello 工作執行的 hello 自動使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="a57fa-116">**具名的使用者帳戶。**</span><span class="sxs-lookup"><span data-stu-id="a57fa-116">**A named user account.**</span></span> <span data-ttu-id="a57fa-117">當您建立 hello 集區時，您可以指定一或多個名稱的使用者帳戶集區。</span><span class="sxs-lookup"><span data-stu-id="a57fa-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="a57fa-118">每個使用者帳戶會建立 hello 集區的每個節點上。</span><span class="sxs-lookup"><span data-stu-id="a57fa-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="a57fa-119">此外 toohello 帳戶名稱，您指定 hello 使用者帳戶密碼，提高權限層級，並針對 Linux 集區，hello SSH 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a57fa-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="a57fa-120">當您新增工作時，您可以指定 hello 名為該工作應該執行的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a57fa-121">hello 批次服務版本 2017年-01-01.4.0 導入了需要您更新您的程式碼 toocall 該版本的重大變更。</span><span class="sxs-lookup"><span data-stu-id="a57fa-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="a57fa-122">如果您是從較舊版本的批次移轉程式碼，請注意該 hello **runElevated** hello REST API 或批次用戶端程式庫中不再支援屬性。</span><span class="sxs-lookup"><span data-stu-id="a57fa-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="a57fa-123">使用新的 hello **userIdentity**工作 toospecify 提高權限層級屬性。</span><span class="sxs-lookup"><span data-stu-id="a57fa-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="a57fa-124">請參閱 < hello > 一節[更新您的程式碼 toohello 最新批次用戶端程式庫](#update-your-code-to-the-latest-batch-client-library)需更新您的批次程式碼，如果您使用其中一個 hello 用戶端程式庫的快速指導方針。</span><span class="sxs-lookup"><span data-stu-id="a57fa-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="a57fa-125">本文所討論的 hello 使用者帳戶不支援遠端桌面通訊協定 (RDP) 或安全殼層 (SSH)，基於安全性考量。</span><span class="sxs-lookup"><span data-stu-id="a57fa-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="a57fa-126">tooconnect tooa 節點執行 hello Linux 虛擬機器中的設定透過 SSH，請參閱[使用遠端桌面 tooa 在 Azure 中的 Linux VM](../virtual-machines/virtual-machines-linux-use-remote-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="a57fa-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="a57fa-127">tooconnect toonodes 執行 Windows，透過 RDP，請參閱[連接 tooa Windows Server VM](../virtual-machines/windows/connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="a57fa-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="a57fa-128">tooconnect tooa 節點執行 hello 雲端服務中的設定透過 RDP，請參閱[Azure 雲端服務中的角色啟用遠端桌面連線](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a57fa-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="a57fa-129">使用者帳戶存取 toofiles 和目錄</span><span class="sxs-lookup"><span data-stu-id="a57fa-129">User account access toofiles and directories</span></span>

<span data-ttu-id="a57fa-130">自動使用者帳戶和名稱的使用者帳戶有讀取/寫入存取 toohello 工作的工作目錄、 共用的目錄和多重執行個體的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="a57fa-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="a57fa-131">這兩種類型的帳戶有讀取權限 toohello 啟動和工作準備的目錄。</span><span class="sxs-lookup"><span data-stu-id="a57fa-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="a57fa-132">如果工作執行下 hello 用於執行啟動工作、 hello 工作的相同帳戶具有讀寫存取 toohello 開始工作目錄。</span><span class="sxs-lookup"><span data-stu-id="a57fa-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="a57fa-133">相同同樣地，hello 如果之下執行的工作執行作業準備工作、 hello 工作所使用的帳戶具有讀寫存取 toohello 作業準備工作目錄。</span><span class="sxs-lookup"><span data-stu-id="a57fa-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="a57fa-134">如果工作執行比 hello 啟動工作或作業準備工作不同的帳戶，然後 hello 工作有只讀取權限 toohello 個別目錄。</span><span class="sxs-lookup"><span data-stu-id="a57fa-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="a57fa-135">如需從工作存取檔案和目錄的相關詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#files-and-directories)。</span><span class="sxs-lookup"><span data-stu-id="a57fa-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="a57fa-136">提高工作的權限</span><span class="sxs-lookup"><span data-stu-id="a57fa-136">Elevated access for tasks</span></span> 

<span data-ttu-id="a57fa-137">hello 使用者帳戶的提高權限層級表示工作是否執行具有提高權限的存取權。</span><span class="sxs-lookup"><span data-stu-id="a57fa-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="a57fa-138">自動使用者帳戶和具名的使用者帳戶都可以使用提高權限的存取權來執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="a57fa-139">提高權限層級的 hello 兩個選項如下：</span><span class="sxs-lookup"><span data-stu-id="a57fa-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="a57fa-140">**NonAdmin:** hello 工作沒有提高權限的存取權的標準使用者身分執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="a57fa-141">批次的使用者帳戶的 hello 預設提高權限層級是一律**NonAdmin**。</span><span class="sxs-lookup"><span data-stu-id="a57fa-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="a57fa-142">**系統管理員：** hello 工作具有提高權限的存取權的使用者身分執行，並且作業具有完整的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="a57fa-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="a57fa-143">自動使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="a57fa-143">Auto-user accounts</span></span>

<span data-ttu-id="a57fa-144">根據預設，Batch 中的工作會在自動使用者帳戶下執行，以標準使用者身分執行，沒有提高權限的存取權，並具有工作範圍。</span><span class="sxs-lookup"><span data-stu-id="a57fa-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="a57fa-145">Hello 自動使用者規格工作範圍的設定時，hello 批次服務會建立只有該工作的自動使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="a57fa-146">hello 替代 tootask 範圍為集區範圍。</span><span class="sxs-lookup"><span data-stu-id="a57fa-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="a57fa-147">Hello 自動使用者規格工作設定為集區範圍，hello 工作會在 hello 集區中的可用 tooany 工作自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="a57fa-148">多個集區範圍的詳細資訊，請參閱 < hello > 一節[執行工作，如 hello 與集區範圍自動使用者](#run-a-task-as-the-autouser-with-pool-scope)。</span><span class="sxs-lookup"><span data-stu-id="a57fa-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="a57fa-149">hello 預設範圍是在不同的 Windows 和 Linux 節點上：</span><span class="sxs-lookup"><span data-stu-id="a57fa-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="a57fa-150">在 Windows 節點上，工作根據預設會在工作範圍下執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="a57fa-151">Linux 節點一律會在集區範圍下執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="a57fa-152">有四個可能的設定 hello 自動使用者規格，其中每個對應 tooa 唯一的自動使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="a57fa-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="a57fa-153">與工作範圍 （hello 預設自動使用者規格） 的非系統管理員存取權</span><span class="sxs-lookup"><span data-stu-id="a57fa-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="a57fa-154">具有工作範圍的系統管理員 (提升權限) 存取權</span><span class="sxs-lookup"><span data-stu-id="a57fa-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="a57fa-155">具有集區範圍的非系統管理員存取權</span><span class="sxs-lookup"><span data-stu-id="a57fa-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="a57fa-156">具有集區範圍的系統管理員存取權</span><span class="sxs-lookup"><span data-stu-id="a57fa-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a57fa-157">工作範圍下執行的工作不需要在節點上的既定存取 tooother 工作。</span><span class="sxs-lookup"><span data-stu-id="a57fa-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="a57fa-158">不過，具有存取 toohello 帳戶的惡意使用者無法解決這項限制提交的工作，以系統管理員權限執行，以及存取其他的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="a57fa-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="a57fa-159">惡意使用者可能也會使用 RDP 或 SSH tooconnect tooa 節點。</span><span class="sxs-lookup"><span data-stu-id="a57fa-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="a57fa-160">很重要的 tooprotect 存取 tooyour 批次帳戶金鑰 tooprevent 這類案例中。</span><span class="sxs-lookup"><span data-stu-id="a57fa-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="a57fa-161">如果您懷疑可能受到危害您的帳戶，是確定 tooregenerate 您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="a57fa-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="a57fa-162">以具有提高權限之存取權的自動使用者身分執行工作</span><span class="sxs-lookup"><span data-stu-id="a57fa-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="a57fa-163">當您需要 toorun 高存取權限的工作時，您可以設定系統管理員權限的 hello 自動使用者規格。</span><span class="sxs-lookup"><span data-stu-id="a57fa-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="a57fa-164">例如，啟動工作可能需要提高權限的存取 tooinstall 軟體 hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="a57fa-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="a57fa-165">一般情況下，建議您最好 toouse 提高權限只在必要時的存取。</span><span class="sxs-lookup"><span data-stu-id="a57fa-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="a57fa-166">最佳作法建議授與 hello 最低權限所需的 tooachieve hello 所要的結果。</span><span class="sxs-lookup"><span data-stu-id="a57fa-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="a57fa-167">比方說，如果啟動工作以安裝軟體 hello 目前的使用者，而不是針對所有使用者，您可能無法授與提高權限的存取 tootasks 的 tooavoid。</span><span class="sxs-lookup"><span data-stu-id="a57fa-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="a57fa-168">您可以設定需要 toorun 下 hello 使用相同帳戶，包括 hello 啟動工作的所有工作的集區範圍和非系統管理員存取權的 hello 自動使用者規格。</span><span class="sxs-lookup"><span data-stu-id="a57fa-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="a57fa-169">hello，下列程式碼片段顯示如何 tooconfigure hello 自動使用者規格。</span><span class="sxs-lookup"><span data-stu-id="a57fa-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="a57fa-170">hello 範例設定 hello 提高權限層級太`Admin`和太 hello 範圍`Task`。</span><span class="sxs-lookup"><span data-stu-id="a57fa-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="a57fa-171">工作範圍 hello 預設設定，但是此處涵蓋了 hello 不錯的範例。</span><span class="sxs-lookup"><span data-stu-id="a57fa-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="a57fa-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="a57fa-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="a57fa-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="a57fa-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="a57fa-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="a57fa-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="a57fa-175">以具有集區範圍的自動使用者身分執行工作</span><span class="sxs-lookup"><span data-stu-id="a57fa-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="a57fa-176">節點會佈建時，會建立兩個整個集區的自動使用者帳戶上 hello 集區中的每個節點，一個具有提高權限的存取權，一個沒有提高權限的存取權。</span><span class="sxs-lookup"><span data-stu-id="a57fa-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="a57fa-177">設定特定工作的 hello 自動為使用者的範圍 toopool 範圍執行 hello 工作，其中兩個整個集區的自動使用者帳戶下。</span><span class="sxs-lookup"><span data-stu-id="a57fa-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="a57fa-178">當您指定 hello 自動使用者集區範圍時，以系統管理員存取權執行的所有工作都執行下 hello 相同整個集區的自動使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="a57fa-179">同樣地，不具系統管理員權限執行的工作，也會在單一的全集區自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="a57fa-180">hello 兩個整個集區的自動使用者帳戶是不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="a57fa-181">Hello 整個集區的系統管理帳戶下執行的工作無法共用資料，與工作執行 hello 標準帳戶，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="a57fa-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="a57fa-182">hello 利用 toorunning hello 工作是與 hello 上執行其他工作能 tooshare 資料的相同的自動使用者帳戶是在相同的節點。</span><span class="sxs-lookup"><span data-stu-id="a57fa-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="a57fa-183">共用工作之間的密碼是一種情況，其中執行的工作在其中兩個 hello 整個集區的自動使用者帳戶底下是很有用。</span><span class="sxs-lookup"><span data-stu-id="a57fa-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="a57fa-184">例如，假設啟動工作需要 tooprovision 到可以使用其他工作的 hello 節點上的密碼。</span><span class="sxs-lookup"><span data-stu-id="a57fa-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="a57fa-185">您可以使用 hello Windows 資料保護 API (DPAPI)，但它需要系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="a57fa-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="a57fa-186">相反地，您可以保護 hello hello 使用者層級的密碼。</span><span class="sxs-lookup"><span data-stu-id="a57fa-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="a57fa-187">工作執行相同的使用者帳戶可以存取的 hello hello 沒有提高權限的存取權的密碼。</span><span class="sxs-lookup"><span data-stu-id="a57fa-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="a57fa-188">另一種情形，您可能需要 toorun 工作與集區範圍自動使用者帳戶是訊息傳遞介面 (MPI) 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="a57fa-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="a57fa-189">MPI 檔案共用時，在 hello MPI 工作需要 toowork 上 hello 節點 hello 相同的檔案資料。</span><span class="sxs-lookup"><span data-stu-id="a57fa-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="a57fa-190">hello 前端節點建立的檔案共用如果 hello 下執行，可以存取 hello 子節點相同的自動使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="a57fa-191">下列程式碼片段的 hello 設定批次.NET hello 自動位使用者的範圍 toopool 範圍的工作。</span><span class="sxs-lookup"><span data-stu-id="a57fa-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="a57fa-192">省略 hello 提高權限層級，因此 hello 工作 hello 標準整個集區的自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="a57fa-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="a57fa-193">具名的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="a57fa-193">Named user accounts</span></span>

<span data-ttu-id="a57fa-194">當您建立集區時，可以定義具名的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="a57fa-195">具名的使用者帳戶具有您提供的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="a57fa-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="a57fa-196">您可以指定名稱的使用者帳戶的 hello 提高權限層級。</span><span class="sxs-lookup"><span data-stu-id="a57fa-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="a57fa-197">您也可以提供適用於 Linux 節點的 SSH 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a57fa-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="a57fa-198">具名的使用者帳戶存在 hello 集區中的所有節點上，且可用 tooall 工作執行那些節點上。</span><span class="sxs-lookup"><span data-stu-id="a57fa-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="a57fa-199">您可以針對集區定義任意數目的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a57fa-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="a57fa-200">當您新增工作或工作集合時，您可以指定其中一個 hello 名為 hello 集區上定義的使用者帳戶執行該 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="a57fa-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="a57fa-201">具名的使用者帳戶是很有用時想 toorun 作業中的所有工作底下 hello 相同的使用者帳戶，但會將從端 hello 其他作業中執行的工作相同的時間。</span><span class="sxs-lookup"><span data-stu-id="a57fa-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="a57fa-202">例如，您可以為每個作業建立具名的使用者，並在該具名的使用者帳戶下執行每個作業的工作。</span><span class="sxs-lookup"><span data-stu-id="a57fa-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="a57fa-203">接著，每個作業可與它自己的工作共用祕密，但不可與其他作業中執行的工作共用祕密。</span><span class="sxs-lookup"><span data-stu-id="a57fa-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="a57fa-204">您也可以使用名稱的使用者帳戶 toorun 外部資源，例如檔案共用設定權限的工作。</span><span class="sxs-lookup"><span data-stu-id="a57fa-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="a57fa-205">使用具名的使用者帳戶，您可以控制 hello 使用者識別，並且可以使用該使用者身分識別 tooset 權限。</span><span class="sxs-lookup"><span data-stu-id="a57fa-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="a57fa-206">具名的使用者帳戶會啟用 Linux 節點之間的無密碼 SSH。</span><span class="sxs-lookup"><span data-stu-id="a57fa-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="a57fa-207">您可以使用名稱的使用者帳戶與 Linux 節點需要 toorun 多重執行個體的工作。</span><span class="sxs-lookup"><span data-stu-id="a57fa-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="a57fa-208">Hello 集區中的每個節點可以執行 hello 整個集區上定義的使用者帳戶的工作。</span><span class="sxs-lookup"><span data-stu-id="a57fa-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="a57fa-209">如需多重執行個體工作的詳細資訊，請參閱[使用多重\-toorun MPI 應用程式的執行個體工作](batch-mpi.md)。</span><span class="sxs-lookup"><span data-stu-id="a57fa-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="a57fa-210">建立具名的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="a57fa-210">Create named user accounts</span></span>

<span data-ttu-id="a57fa-211">toocreate 名為批次中的使用者帳戶新增使用者帳戶 toohello 集區的集合。</span><span class="sxs-lookup"><span data-stu-id="a57fa-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="a57fa-212">hello 下列程式碼片段顯示如何 toocreate 命名.NET、 Java 和 Python 中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="a57fa-213">這些程式碼片段顯示如何 toocreate 管理員和非管理員帳戶的集區上名為。</span><span class="sxs-lookup"><span data-stu-id="a57fa-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="a57fa-214">hello 範例會建立集區使用 hello 雲端服務組態，但使用相同方法時建立 Windows 或 Linux 的集區，使用 hello 虛擬機器組態的 hello。</span><span class="sxs-lookup"><span data-stu-id="a57fa-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="a57fa-215">Batch .NET 範例 (Windows)</span><span class="sxs-lookup"><span data-stu-id="a57fa-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="a57fa-216">Batch .NET 範例 (Linux)</span><span class="sxs-lookup"><span data-stu-id="a57fa-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="a57fa-217">Batch Java 範例</span><span class="sxs-lookup"><span data-stu-id="a57fa-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="a57fa-218">Batch Python 範例</span><span class="sxs-lookup"><span data-stu-id="a57fa-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="a57fa-219">在具有提高權限之存取權的具名使用者帳戶下執行工作</span><span class="sxs-lookup"><span data-stu-id="a57fa-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="a57fa-220">以提高的使用者，hello 任務的任務 toorun **UserIdentity**屬性 tooa 名為所建立的使用者帳戶其**ElevationLevel**屬性設定太`Admin`。</span><span class="sxs-lookup"><span data-stu-id="a57fa-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="a57fa-221">此程式碼片段會指定該 hello 工作應該執行具名的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a57fa-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="a57fa-222">建立 hello 集區時，此名稱的使用者帳戶已定義 hello 集區上。</span><span class="sxs-lookup"><span data-stu-id="a57fa-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="a57fa-223">在此情況下，建立名為使用者帳戶的 hello 與系統管理員權限：</span><span class="sxs-lookup"><span data-stu-id="a57fa-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="a57fa-224">更新您的程式碼 toohello 最新批次用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="a57fa-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="a57fa-225">2017-01-01.4.0 導入了一項重大變更，取代 hello hello 批次服務版本**runElevated**屬性可用在舊版本中以 hello **userIdentity**屬性。</span><span class="sxs-lookup"><span data-stu-id="a57fa-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="a57fa-226">下表中的 hello 提供簡單的對應，您可以使用 tooupdate hello 用戶端程式庫的舊版程式碼。</span><span class="sxs-lookup"><span data-stu-id="a57fa-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="a57fa-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="a57fa-227">Batch .NET</span></span>

| <span data-ttu-id="a57fa-228">如果您的程式碼使用...</span><span class="sxs-lookup"><span data-stu-id="a57fa-228">If your code uses...</span></span>                  | <span data-ttu-id="a57fa-229">將它更新為...</span><span class="sxs-lookup"><span data-stu-id="a57fa-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="a57fa-230">`CloudTask.RunElevated` 未指定</span><span class="sxs-lookup"><span data-stu-id="a57fa-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="a57fa-231">不需要更新</span><span class="sxs-lookup"><span data-stu-id="a57fa-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="a57fa-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="a57fa-232">Batch Java</span></span>

| <span data-ttu-id="a57fa-233">如果您的程式碼使用...</span><span class="sxs-lookup"><span data-stu-id="a57fa-233">If your code uses...</span></span>                      | <span data-ttu-id="a57fa-234">將它更新為...</span><span class="sxs-lookup"><span data-stu-id="a57fa-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="a57fa-235">`CloudTask.withRunElevated` 未指定</span><span class="sxs-lookup"><span data-stu-id="a57fa-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="a57fa-236">不需要更新</span><span class="sxs-lookup"><span data-stu-id="a57fa-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="a57fa-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="a57fa-237">Batch Python</span></span>

| <span data-ttu-id="a57fa-238">如果您的程式碼使用...</span><span class="sxs-lookup"><span data-stu-id="a57fa-238">If your code uses...</span></span>                      | <span data-ttu-id="a57fa-239">將它更新為...</span><span class="sxs-lookup"><span data-stu-id="a57fa-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="a57fa-240">`user_identity=user`，其中</span><span class="sxs-lookup"><span data-stu-id="a57fa-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="a57fa-241">`user_identity=user`，其中</span><span class="sxs-lookup"><span data-stu-id="a57fa-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="a57fa-242">`run_elevated` 未指定</span><span class="sxs-lookup"><span data-stu-id="a57fa-242">`run_elevated` not specified</span></span> | <span data-ttu-id="a57fa-243">不需要更新</span><span class="sxs-lookup"><span data-stu-id="a57fa-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="a57fa-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a57fa-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="a57fa-245">Batch 論壇</span><span class="sxs-lookup"><span data-stu-id="a57fa-245">Batch Forum</span></span>

<span data-ttu-id="a57fa-246">hello [Azure Batch 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)MSDN 上會很大的放置 toodiscuss 批次，並詢問 hello 服務有關的問題。</span><span class="sxs-lookup"><span data-stu-id="a57fa-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="a57fa-247">請前去查看很有幫助的釘選文章，在建立 Batch 解決方案時，出現問題就張貼。</span><span class="sxs-lookup"><span data-stu-id="a57fa-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
