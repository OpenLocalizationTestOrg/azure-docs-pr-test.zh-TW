---
title: "在 Azure Batch 中的使用者帳戶執行工作 | Microsoft Docs"
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
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="0fb7d-103">在 Batch 中的使用者帳戶執行工作</span><span class="sxs-lookup"><span data-stu-id="0fb7d-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="0fb7d-104">Azure Batch 中的工作一律會在使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="0fb7d-105">根據預設，會在標準使用者帳戶中執行工作，而不需要系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="0fb7d-106">這些預設使用者帳戶設定通常已足夠。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="0fb7d-107">不過，在特定案例中，最好能夠在您想要執行工作的使用者帳戶進行設定。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="0fb7d-108">本文討論使用者帳戶的類型，以及如何針對您的案例來設定它們。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="0fb7d-109">使用者帳戶的類型</span><span class="sxs-lookup"><span data-stu-id="0fb7d-109">Types of user accounts</span></span>

<span data-ttu-id="0fb7d-110">Azure Batch 提供執行工作所需的兩種使用者帳戶類型︰</span><span class="sxs-lookup"><span data-stu-id="0fb7d-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="0fb7d-111">**自動使用者帳戶。**</span><span class="sxs-lookup"><span data-stu-id="0fb7d-111">**Auto-user accounts.**</span></span> <span data-ttu-id="0fb7d-112">自動使用者帳戶是由 Batch 服務自動建立的內建使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="0fb7d-113">根據預設，工作會在自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="0fb7d-114">您可以針對工作設定自動使用者規格，來表示工作應該在哪一個自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="0fb7d-115">自動使用者規格可讓您指定執行工作之自動使用者帳戶的範圍及提高權限層級。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="0fb7d-116">**具名的使用者帳戶。**</span><span class="sxs-lookup"><span data-stu-id="0fb7d-116">**A named user account.**</span></span> <span data-ttu-id="0fb7d-117">當您建立集區時，可以指定一或多個集區的具名使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="0fb7d-118">每個使用者帳戶都會建立在集區的每個節點上。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="0fb7d-119">除了帳戶名稱之外，您會指定使用者帳戶密碼、提高權限層級，以及針對 Linux 集區指定 SSH 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="0fb7d-120">當您新增一項工作時，可以指定應執行該工作的具名使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0fb7d-121">Batch 服務版本 2017-01-01.4.0 導入了重大變更，要求您更新程式碼以呼叫該版本。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="0fb7d-122">如果您是從較舊版本的 Batch 移轉程式碼，請注意，REST API 或 Batch 用戶端程式庫不再支援 **runElevated** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="0fb7d-123">使用工作的新 **userIdentity** 屬性來指定提高權限層級。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="0fb7d-124">如果您使用的是其中一個用戶端程式庫，請參閱標題為[將您的程式碼更新至最新的 Batch 用戶端程式庫](#update-your-code-to-the-latest-batch-client-library)的章節，以取得更新 Batch 程式碼的快速指導方針。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="0fb7d-125">基於安全性考量，本文所討論的使用者帳戶不支援遠端桌面通訊協定 (RDP) 或安全殼層 (SSH)。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="0fb7d-126">若要連線到透過 SSH 執行 Linux 虛擬機器設定的節點，請參閱[在 Azure 中使用 Linux VM 的遠端桌面](../virtual-machines/virtual-machines-linux-use-remote-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="0fb7d-127">若要連線到透過 RDP 執行 Windows 的節點，請參閱[連線到 Windows Server VM](../virtual-machines/windows/connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="0fb7d-128">若要連線到透過 RDP 執行雲端服務設定的節點，請參閱[在 Azure 雲端服務中啟用角色的遠端桌面連線](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="0fb7d-129">使用者帳戶存取檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="0fb7d-129">User account access to files and directories</span></span>

<span data-ttu-id="0fb7d-130">自動使用者帳戶和具名的使用者帳戶具有讀取/寫入權限，可存取工作的工作目錄、共用的目錄和多重執行個體的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="0fb7d-131">這兩種類型的帳戶都具有啟動和作業準備工作目錄的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="0fb7d-132">如果相同帳戶下執行的工作用來執行啟動工作，則工作具有啟動工作目錄的讀寫權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="0fb7d-133">同樣地，如果相同帳戶下執行的工作用來執行作業準備工作，則工作具有作業準備工作目錄的讀寫權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="0fb7d-134">如果是在與啟動工作或作業準備工作不同的帳戶下執行工作，則工作只有個別目錄的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="0fb7d-135">如需從工作存取檔案和目錄的相關詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#files-and-directories)。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="0fb7d-136">提高工作的權限</span><span class="sxs-lookup"><span data-stu-id="0fb7d-136">Elevated access for tasks</span></span> 

<span data-ttu-id="0fb7d-137">使用者帳戶的提高權限層級會表示工作是否使用提高權限的存取權來執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="0fb7d-138">自動使用者帳戶和具名的使用者帳戶都可以使用提高權限的存取權來執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="0fb7d-139">提高權限層級的兩個選項如下︰</span><span class="sxs-lookup"><span data-stu-id="0fb7d-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="0fb7d-140">**NonAdmin：**工作是以標準使用者身分執行，沒有提高權限的存取權。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="0fb7d-141">Batch 使用者帳戶的預設提高權限層級一律為 **NonAdmin**。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="0fb7d-142">**系統管理員︰**工作是以具有提高權限存取權的使用者身分執行，並以完整系統管理員權限運作。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="0fb7d-143">自動使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="0fb7d-143">Auto-user accounts</span></span>

<span data-ttu-id="0fb7d-144">根據預設，Batch 中的工作會在自動使用者帳戶下執行，以標準使用者身分執行，沒有提高權限的存取權，並具有工作範圍。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="0fb7d-145">針對工作範圍設定自動使用者規格之後，Batch 服務只會建立該工作的自動使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="0fb7d-146">工作範圍的替代方案是集區範圍。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="0fb7d-147">當針對集區範圍設定工作的自動使用者規格時，會在集區中任何工作可用的自動使用者帳戶下執行工作。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="0fb7d-148">如需集區範圍的詳細資訊，請參閱標題為[以自動使用者身分在集區範圍中執行工作](#run-a-task-as-the-autouser-with-pool-scope)的章節。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="0fb7d-149">預設範圍在 Windows 和 Linux 節點上有所差異︰</span><span class="sxs-lookup"><span data-stu-id="0fb7d-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="0fb7d-150">在 Windows 節點上，工作根據預設會在工作範圍下執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="0fb7d-151">Linux 節點一律會在集區範圍下執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="0fb7d-152">自動使用者規格有四個可能的設定，其中每一個都對應至唯一的自動使用者帳戶︰</span><span class="sxs-lookup"><span data-stu-id="0fb7d-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="0fb7d-153">具有工作範圍 (預設的自動使用者規格) 的非系統管理員存取權</span><span class="sxs-lookup"><span data-stu-id="0fb7d-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="0fb7d-154">具有工作範圍的系統管理員 (提升權限) 存取權</span><span class="sxs-lookup"><span data-stu-id="0fb7d-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="0fb7d-155">具有集區範圍的非系統管理員存取權</span><span class="sxs-lookup"><span data-stu-id="0fb7d-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="0fb7d-156">具有集區範圍的系統管理員存取權</span><span class="sxs-lookup"><span data-stu-id="0fb7d-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0fb7d-157">在工作範圍下執行的工作沒有節點上其他工作的既定存取權。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="0fb7d-158">不過，具有帳戶存取權的惡意使用者只要提交以系統管理員權限執行的工作，並存取其他的工作目錄，便可以解決這項限制。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="0fb7d-159">惡意使用者也可以使用 RDP 或 SSH 連線到節點。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="0fb7d-160">請務必保護您 Batch 帳戶金鑰的存取權，以避免發生此情況。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="0fb7d-161">如果您懷疑您的帳戶已遭入侵，請務必重新產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="0fb7d-162">以具有提高權限之存取權的自動使用者身分執行工作</span><span class="sxs-lookup"><span data-stu-id="0fb7d-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="0fb7d-163">當您需要以提高權限的存取權執行工作時，可以針對系統管理員權限設定自動使用者規格。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="0fb7d-164">例如，啟動工作可能需要提高權限的存取權才可在節點上安裝軟體。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="0fb7d-165">一般而言，最好只在必要時才使用提高權限的存取。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="0fb7d-166">最佳做法建議授與達成所需結果所需的最低權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="0fb7d-167">例如，如果啟動工作為目前的使用者而不是所有使用者安裝軟體，您可能會避免將提高權限的存取權授與給工作。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="0fb7d-168">您可以針對集區範圍設定自動使用者規格，以及針對需要在相同帳戶中執行的所有工作 (包括啟動工作) 設定非系統管理員存取權。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="0fb7d-169">下列程式碼片段示範如何設定自動使用者規格。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="0fb7d-170">範例會將提高權限層級設定為 `Admin`，以及將範圍設定為 `Task`。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="0fb7d-171">工作範圍是預設設定，但是也包含在此作為範例。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="0fb7d-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="0fb7d-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="0fb7d-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="0fb7d-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="0fb7d-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="0fb7d-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="0fb7d-175">以具有集區範圍的自動使用者身分執行工作</span><span class="sxs-lookup"><span data-stu-id="0fb7d-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="0fb7d-176">當佈建節點時，會在集區的每個節點上建立兩個全集區的自動使用者帳戶，一個具有提高權限的存取權，另一個則沒有提高權限的存取權。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="0fb7d-177">將自動使用者的範圍設為特定工作的集區範圍，會在兩個全集區的自動使用者帳戶其中之一執行工作。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="0fb7d-178">當您指定自動使用者的集區範圍時，使用系統管理員存取權執行的所有工作，會在相同的全集區自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="0fb7d-179">同樣地，不具系統管理員權限執行的工作，也會在單一的全集區自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="0fb7d-180">這兩個全集區的自動使用者帳戶是不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="0fb7d-181">在全集區的系統管理帳戶下執行的工作，不能與標準帳戶下執行的工作共用資料，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="0fb7d-182">在相同自動使用者帳戶下執行的優點是，工作都能與相同節點上執行的其他工作共用資料。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="0fb7d-183">在工作之間共用祕密這個案例中，在兩個全集區的自動使用者帳戶其中之一執行工作會很實用。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="0fb7d-184">例如，假設啟動工作需要將祕密佈建到其他工作可以使用的節點上。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="0fb7d-185">您可以使用 Windows 資料保護 API (DPAPI)，但它需要系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="0fb7d-186">相反地，您可以保護使用者層級的祕密。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="0fb7d-187">在相同使用者帳戶下執行的工作，無需提高權限的存取即可存取祕密。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="0fb7d-188">您可能要在集區範圍的自動使用者帳戶執行工作的另一種情況，是訊息傳遞介面 (MPI) 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="0fb7d-189">當 MPI 工作中的節點必須使用相同的檔案資料時，MPI 檔案共用便很有用。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="0fb7d-190">如果子節點是在相同的自動使用者帳戶下執行，前端節點會建立子節點可以存取的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="0fb7d-191">下列程式碼片段會將自動使用者的範圍設為 Batch .NET 中的工作集區範圍。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="0fb7d-192">提高權限層級會予以省略，因此工作會在標準全集區的自動使用者帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="0fb7d-193">具名的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="0fb7d-193">Named user accounts</span></span>

<span data-ttu-id="0fb7d-194">當您建立集區時，可以定義具名的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="0fb7d-195">具名的使用者帳戶具有您提供的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="0fb7d-196">您可以指定具名使用者帳戶的提高權限層級。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="0fb7d-197">您也可以提供適用於 Linux 節點的 SSH 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="0fb7d-198">具名的使用者帳戶存在於集區中的所有節點上，且可在這些節點上執行的所有工作上使用。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="0fb7d-199">您可以針對集區定義任意數目的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="0fb7d-200">當您新增工作或工作集合時，可以指定要在集區上定義之其中一個具名使用者帳戶下執行的工作。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="0fb7d-201">當您想要在相同使用者帳戶下執行作業中的所有工作，而同時要將這些工作與其他作業中執行的工作隔離時，具名的使用者帳戶便很有用。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="0fb7d-202">例如，您可以為每個作業建立具名的使用者，並在該具名的使用者帳戶下執行每個作業的工作。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="0fb7d-203">接著，每個作業可與它自己的工作共用祕密，但不可與其他作業中執行的工作共用祕密。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="0fb7d-204">您也可以使用具名的使用者帳戶來執行工作，其會設定外部資源 (例如檔案共用) 上的設定權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="0fb7d-205">使用具名的使用者帳戶，您可以控制使用者身分識別，且可以使用該使用者身分識別來設定權限。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="0fb7d-206">具名的使用者帳戶會啟用 Linux 節點之間的無密碼 SSH。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="0fb7d-207">您可以搭配使用具名的使用者帳戶與需要執行多個執行個體工作的 Linux 節點。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="0fb7d-208">集區中的每個節點都可以在整個集區上定義的使用者帳戶內執行工作。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="0fb7d-209">如需多個執行個體工作的詳細資訊，請參閱[使用多重\-執行個體工作來執行 MPI 應用程式](batch-mpi.md)。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="0fb7d-210">建立具名的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="0fb7d-210">Create named user accounts</span></span>

<span data-ttu-id="0fb7d-211">若要在 Batch 中建立具名使用者帳戶，請將使用者帳戶的集合新增至集區。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="0fb7d-212">下列程式碼片段示範如何在 .NET、Java 和 Python 建立具名的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="0fb7d-213">這些程式碼片段示範如何在集區上建立系統管理員和非系統管理員的具名帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="0fb7d-214">範例會使用雲端服務設定來建立集區，但當您使用虛擬機器設定來建立 Windows 或 Linux 集區時，才使用相同的方法。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="0fb7d-215">Batch .NET 範例 (Windows)</span><span class="sxs-lookup"><span data-stu-id="0fb7d-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
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

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="0fb7d-216">Batch .NET 範例 (Linux)</span><span class="sxs-lookup"><span data-stu-id="0fb7d-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
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

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="0fb7d-217">Batch Java 範例</span><span class="sxs-lookup"><span data-stu-id="0fb7d-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="0fb7d-218">Batch Python 範例</span><span class="sxs-lookup"><span data-stu-id="0fb7d-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="0fb7d-219">在具有提高權限之存取權的具名使用者帳戶下執行工作</span><span class="sxs-lookup"><span data-stu-id="0fb7d-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="0fb7d-220">若要以提高權限的使用者身分執行工作，將工作的 **UserIdentity** 屬性設定為建立時將 **ElevationLevel** 屬性設定為 `Admin` 的具名使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="0fb7d-221">此程式碼片段會指定須在具名的使用者帳戶下執行工作。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="0fb7d-222">集區建立時，會在集區上定義此具名的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="0fb7d-223">在此情況下，會使用系統管理員權限來建立具名的使用者帳戶︰</span><span class="sxs-lookup"><span data-stu-id="0fb7d-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="0fb7d-224">將程式碼更新至最新的 Batch 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="0fb7d-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="0fb7d-225">Batch 服務版本 2017-01-01.4.0 導入重大變更，將舊版中的 **runElevated** 屬性取代為 **userIdentity** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="0fb7d-226">下表提供的簡單對應可供您用來將舊版的用戶端程式庫的程式碼進行更新。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="0fb7d-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="0fb7d-227">Batch .NET</span></span>

| <span data-ttu-id="0fb7d-228">如果您的程式碼使用...</span><span class="sxs-lookup"><span data-stu-id="0fb7d-228">If your code uses...</span></span>                  | <span data-ttu-id="0fb7d-229">將它更新為...</span><span class="sxs-lookup"><span data-stu-id="0fb7d-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="0fb7d-230">`CloudTask.RunElevated` 未指定</span><span class="sxs-lookup"><span data-stu-id="0fb7d-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="0fb7d-231">不需要更新</span><span class="sxs-lookup"><span data-stu-id="0fb7d-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="0fb7d-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="0fb7d-232">Batch Java</span></span>

| <span data-ttu-id="0fb7d-233">如果您的程式碼使用...</span><span class="sxs-lookup"><span data-stu-id="0fb7d-233">If your code uses...</span></span>                      | <span data-ttu-id="0fb7d-234">將它更新為...</span><span class="sxs-lookup"><span data-stu-id="0fb7d-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="0fb7d-235">`CloudTask.withRunElevated` 未指定</span><span class="sxs-lookup"><span data-stu-id="0fb7d-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="0fb7d-236">不需要更新</span><span class="sxs-lookup"><span data-stu-id="0fb7d-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="0fb7d-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="0fb7d-237">Batch Python</span></span>

| <span data-ttu-id="0fb7d-238">如果您的程式碼使用...</span><span class="sxs-lookup"><span data-stu-id="0fb7d-238">If your code uses...</span></span>                      | <span data-ttu-id="0fb7d-239">將它更新為...</span><span class="sxs-lookup"><span data-stu-id="0fb7d-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="0fb7d-240">`user_identity=user`，其中</span><span class="sxs-lookup"><span data-stu-id="0fb7d-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="0fb7d-241">`user_identity=user`，其中</span><span class="sxs-lookup"><span data-stu-id="0fb7d-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="0fb7d-242">`run_elevated` 未指定</span><span class="sxs-lookup"><span data-stu-id="0fb7d-242">`run_elevated` not specified</span></span> | <span data-ttu-id="0fb7d-243">不需要更新</span><span class="sxs-lookup"><span data-stu-id="0fb7d-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="0fb7d-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fb7d-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="0fb7d-245">Batch 論壇</span><span class="sxs-lookup"><span data-stu-id="0fb7d-245">Batch Forum</span></span>

<span data-ttu-id="0fb7d-246">MSDN 上的 [Azure Batch 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)是一個很棒的地方，可以討論 Batch 和詢問有關此服務的問題。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="0fb7d-247">請前去查看很有幫助的釘選文章，在建立 Batch 解決方案時，出現問題就張貼。</span><span class="sxs-lookup"><span data-stu-id="0fb7d-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>