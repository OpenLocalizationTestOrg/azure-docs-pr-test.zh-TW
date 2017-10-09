---
title: "aaaAdd Azure 自動化 runbook toorecovery 計劃在 hello 傳統入口網站 |Microsoft 文件"
description: "本文說明如何 Azure Site Recovery 現在可讓您使用 Azure 自動化 toocomplete 複雜的工作期間復原 tooAzure tooextend 復原計劃"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="aaa20-103">在 hello 傳統入口網站中加入 Azure 自動化 runbook toorecovery 計劃</span><span class="sxs-lookup"><span data-stu-id="aaa20-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="aaa20-104">本教學課程說明如何與 Azure 自動化 tooprovide 擴充性 toorecovery 計劃整合 Azure Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="aaa20-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="aaa20-105">復原計劃，便可調整的虛擬機器複寫 toosecondary 雲端和複寫 tooAzure 案例使用 Azure Site Recovery 保護的復原。</span><span class="sxs-lookup"><span data-stu-id="aaa20-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="aaa20-106">它們也可以協助進行 hello 復原**一致精確**， **repeatable**，和**自動化**。</span><span class="sxs-lookup"><span data-stu-id="aaa20-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="aaa20-107">如果您容錯移轉虛擬機器 tooAzure，整合 Azure 自動化與擴充的復原計劃，並提供功能 tooexecute runbook，如此可讓功能強大的自動化工作。</span><span class="sxs-lookup"><span data-stu-id="aaa20-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="aaa20-108">如果您還沒聽過「Azure 自動化」，請在[這裡](https://azure.microsoft.com/services/automation/)註冊，然後從[這裡](https://azure.microsoft.com/documentation/scripts/)下載其範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="aaa20-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="aaa20-109">深入了解[Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)和 tooorchestrate 復原 tooAzure 使用復原的計劃[這裡](https://azure.microsoft.com/blog/?p=166264)。</span><span class="sxs-lookup"><span data-stu-id="aaa20-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="aaa20-110">在本簡短教學課程中，我們將會探討如何將 Azure 自動化 Runbook 整合到復原計畫。</span><span class="sxs-lookup"><span data-stu-id="aaa20-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="aaa20-111">我們將自動化先前需要手動介入的簡單工作，請參閱如何 tooconvert 多逐步執行單鍵復原動作的復原。</span><span class="sxs-lookup"><span data-stu-id="aaa20-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="aaa20-112">我們也將探討簡單的指令碼發生錯誤時如何進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="aaa20-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="aaa20-113">保護 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="aaa20-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="aaa20-114">讓我們從兩部虛擬機器所組成的簡單應用程式開始。</span><span class="sxs-lookup"><span data-stu-id="aaa20-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="aaa20-115">在這裡，我們有 Fabrikam 的 HRweb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aaa20-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="aaa20-116">Fabrikam-HRweb-前端和後 Hrweb Fabrikam 端是 hello 兩部虛擬機器保護 tooAzure 使用 Azure Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="aaa20-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="aaa20-117">tooprotect hello 虛擬機器使用 Azure Site Recovery，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="aaa20-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="aaa20-118">對虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="aaa20-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="aaa20-119">請 hello 虛擬機器已完成初始複寫，且會複寫。</span><span class="sxs-lookup"><span data-stu-id="aaa20-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="aaa20-120">等候直到 hello 初始複寫完成，並 hello 複寫狀態會顯示受保護。</span><span class="sxs-lookup"><span data-stu-id="aaa20-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="aaa20-121">在本教學課程中，我們將建立 Fabrikam HRweb 應用程式 toofailover hello 應用程式 tooAzure hello 的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="aaa20-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="aaa20-122">然後我們會將它整合與 runbook 會在容錯移轉連接埠 80 的 Azure 虛擬機器 tooserve web 網頁的 hello 上建立端點。</span><span class="sxs-lookup"><span data-stu-id="aaa20-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="aaa20-123">首先，讓我們為應用程式建立一個復原計畫。</span><span class="sxs-lookup"><span data-stu-id="aaa20-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="aaa20-124">建立 hello 復原計劃</span><span class="sxs-lookup"><span data-stu-id="aaa20-124">Create hello recovery plan</span></span>
<span data-ttu-id="aaa20-125">toorecover hello 應用程式 tooAzure，您需要 toocreate 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="aaa20-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="aaa20-126">使用 復原方案，您可以指定復原的虛擬機器的 hello 順序。</span><span class="sxs-lookup"><span data-stu-id="aaa20-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="aaa20-127">hello 放置在群組 1 中的虛擬機器會復原並啟動第一個，並會遵照 hello 群組 2 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aaa20-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="aaa20-128">建立一個如下的復原計畫。</span><span class="sxs-lookup"><span data-stu-id="aaa20-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="aaa20-129">深入了解復原計劃，請閱讀文件 tooread[這裡](https://msdn.microsoft.com/library/azure/dn788799.aspx "這裡")。</span><span class="sxs-lookup"><span data-stu-id="aaa20-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="aaa20-130">接下來，讓我們來建立必要的成品 hello Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="aaa20-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="aaa20-131">建立 hello 自動化帳戶和其資產</span><span class="sxs-lookup"><span data-stu-id="aaa20-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="aaa20-132">您需要 Azure 自動化帳戶 toocreate runbook。</span><span class="sxs-lookup"><span data-stu-id="aaa20-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="aaa20-133">如果您沒有帳戶，請瀏覽 tooAzure 自動化索引標籤，以表示![](media/site-recovery-runbook-automation/02.png)並建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="aaa20-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="aaa20-134">授與 hello 帳戶與名稱 tooidentify。</span><span class="sxs-lookup"><span data-stu-id="aaa20-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="aaa20-135">指定要讓 tooplace hello 帳戶的地理區域。</span><span class="sxs-lookup"><span data-stu-id="aaa20-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="aaa20-136">建議您在 hello tooplace hello 帳戶與 hello ASR 保存庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="aaa20-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="aaa20-137">接下來，建立 hello 遵循 hello 帳戶中的資產。</span><span class="sxs-lookup"><span data-stu-id="aaa20-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="aaa20-138">將訂用帳戶名稱新增為資產</span><span class="sxs-lookup"><span data-stu-id="aaa20-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="aaa20-139">加入新的設定![](media/site-recovery-runbook-automation/04.png)在 hello Azure 自動化資產，並選取 太![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="aaa20-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="aaa20-140">選取 hello 變數類型為**字串**</span><span class="sxs-lookup"><span data-stu-id="aaa20-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="aaa20-141">將變數名稱指定為 **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="aaa20-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="aaa20-142">您實際的 Azure 訂用帳戶名稱指定為 hello 變數值。</span><span class="sxs-lookup"><span data-stu-id="aaa20-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="aaa20-143">您可以識別您的訂用帳戶，從您的帳戶在 hello Azure 入口網站上的 hello 設定頁面 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="aaa20-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="aaa20-144">將 Azure 登入認證新增為資產</span><span class="sxs-lookup"><span data-stu-id="aaa20-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="aaa20-145">Azure 自動化會使用 Azure PowerShell tooconnect toothe 訂用帳戶，並那里 hello 成品上運作。</span><span class="sxs-lookup"><span data-stu-id="aaa20-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="aaa20-146">因此，您必須使用您的 Microsoft 帳戶或工作或學校帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="aaa20-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="aaa20-147">您可以安全地使用 hello runbook 資產 toobe 儲存 hello 帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="aaa20-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="aaa20-148">加入新的設定![](media/site-recovery-runbook-automation/04.png)在 hello Azure 自動化資產，並選取![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="aaa20-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="aaa20-149">選取 hello 認證類型為**Windows PowerShell 認證**</span><span class="sxs-lookup"><span data-stu-id="aaa20-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="aaa20-150">Hello 名稱指定為**AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="aaa20-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="aaa20-151">指定 hello 使用者名稱和 toosign 入與密碼。</span><span class="sxs-lookup"><span data-stu-id="aaa20-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="aaa20-152">現在，這兩個設定都可以在您的資產中使用。</span><span class="sxs-lookup"><span data-stu-id="aaa20-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="aaa20-153">如何指定透過 PowerShell tooconnect tooyour 訂用帳戶的詳細資訊[這裡](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="aaa20-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="aaa20-154">接下來，您將可以新增 hello 前端的虛擬機器的端點容錯移轉後的 Azure 自動化中建立 runbook。</span><span class="sxs-lookup"><span data-stu-id="aaa20-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="aaa20-155">Azure 自動化內容</span><span class="sxs-lookup"><span data-stu-id="aaa20-155">Azure automation context</span></span>
<span data-ttu-id="aaa20-156">ASR 將傳遞內容變數 toohello runbook toohelp 您撰寫具有決定性的指令碼。</span><span class="sxs-lookup"><span data-stu-id="aaa20-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="aaa20-157">其中一個可以說 hello 雲端服務和虛擬機器 hello hello 名稱，可預測，但是發生，它不一定與 toocertain 案例，例如其中一個位置 hello 虛擬機器名稱 hello 名稱可能已變更到期 hello hello 案例在 Azure 中的 toounsupported 字元。</span><span class="sxs-lookup"><span data-stu-id="aaa20-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="aaa20-158">因此這項資訊會傳遞 toohello ASR 復原方案一部分 hello*內容*。</span><span class="sxs-lookup"><span data-stu-id="aaa20-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="aaa20-159">以下是範例的 hello 內容變數的外觀。</span><span class="sxs-lookup"><span data-stu-id="aaa20-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="aaa20-160">hello 表包含 hello 內容中的每個變數的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="aaa20-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="aaa20-161">**變數名稱**</span><span class="sxs-lookup"><span data-stu-id="aaa20-161">**Variable name**</span></span> | <span data-ttu-id="aaa20-162">**說明**</span><span class="sxs-lookup"><span data-stu-id="aaa20-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="aaa20-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="aaa20-163">RecoveryPlanName</span></span> |<span data-ttu-id="aaa20-164">正在執行的計劃名稱。</span><span class="sxs-lookup"><span data-stu-id="aaa20-164">Name of plan being run.</span></span> <span data-ttu-id="aaa20-165">可協助您根據採取動作名稱使用 hello 相同指令碼</span><span class="sxs-lookup"><span data-stu-id="aaa20-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="aaa20-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="aaa20-166">FailoverType</span></span> |<span data-ttu-id="aaa20-167">指定是否 hello 容錯移轉是測試、 已規劃或非計劃。</span><span class="sxs-lookup"><span data-stu-id="aaa20-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="aaa20-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="aaa20-168">FailoverDirection</span></span> |<span data-ttu-id="aaa20-169">指定復原 tooprimary 或次要資料庫</span><span class="sxs-lookup"><span data-stu-id="aaa20-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="aaa20-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="aaa20-170">GroupID</span></span> |<span data-ttu-id="aaa20-171">Hello 計劃執行時，找出 hello hello 復原計劃中的群組編號</span><span class="sxs-lookup"><span data-stu-id="aaa20-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="aaa20-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="aaa20-172">VmMap</span></span> |<span data-ttu-id="aaa20-173">Hello 群組中的所有 hello 虛擬機器的陣列</span><span class="sxs-lookup"><span data-stu-id="aaa20-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="aaa20-174">VMMap 索引鍵</span><span class="sxs-lookup"><span data-stu-id="aaa20-174">VMMap key</span></span> |<span data-ttu-id="aaa20-175">每個 VM 的唯一索引鍵 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="aaa20-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="aaa20-176">具有 hello 與適用的 hello VMM hello 虛擬機器識別碼相同。</span><span class="sxs-lookup"><span data-stu-id="aaa20-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="aaa20-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="aaa20-177">RoleName</span></span> |<span data-ttu-id="aaa20-178">Hello 要復原的 Azure VM 的名稱</span><span class="sxs-lookup"><span data-stu-id="aaa20-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="aaa20-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="aaa20-179">CloudServiceName</span></span> |<span data-ttu-id="aaa20-180">哪些 hello 下建立虛擬機器的 azure 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="aaa20-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="aaa20-181">您也可以移至 ASR toohello VM 屬性頁面，並查看 hello VM GUID 屬性的 hello 內容中 tooidentify hello VmMap 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="aaa20-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="aaa20-182">撰寫自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="aaa20-182">Author an Automation runbook</span></span>
<span data-ttu-id="aaa20-183">現在 hello 前端的虛擬機器上建立 hello runbook tooopen 連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="aaa20-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="aaa20-184">在 hello hello 名稱 Azure 自動化帳戶中建立新的 runbook **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="aaa20-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="aaa20-185">瀏覽 toohello hello runbook 作者檢視，然後輸入 hello 草稿模式。</span><span class="sxs-lookup"><span data-stu-id="aaa20-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="aaa20-186">先指定 hello 變數 toouse hello 復原計劃內容</span><span class="sxs-lookup"><span data-stu-id="aaa20-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="aaa20-187">接下來連接 toohello 訂用帳戶使用 hello 認證和訂用帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="aaa20-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="aaa20-188">請注意，您會使用 hello Azure 資產 – **AzureCredential**和**AzureSubscriptionName**這裡。</span><span class="sxs-lookup"><span data-stu-id="aaa20-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="aaa20-189">現在指定 hello 端點詳細資料，然後 hello hello 想 tooexpose hello 端點的虛擬機器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="aaa20-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="aaa20-190">在此案例的 hello 前端虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aaa20-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="aaa20-191">這會指定 hello Azure 端點通訊協定、 hello VM 上的本機連接埠和其對應的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="aaa20-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="aaa20-192">這些變數是參數的所需的 hello Azure 加入端點 tooVMs 的命令。</span><span class="sxs-lookup"><span data-stu-id="aaa20-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="aaa20-193">hello VMGUID 保存 hello hello 需要 toooperate 的虛擬機器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="aaa20-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="aaa20-194">hello 指令碼現在會擷取指定的 VM GUID hello hello 內容，並被它參考的 hello 虛擬機器上建立端點。</span><span class="sxs-lookup"><span data-stu-id="aaa20-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="aaa20-195">一旦完成，叫用發佈![](media/site-recovery-runbook-automation/20.png)tooallow 您指令碼 toobe 可供執行。</span><span class="sxs-lookup"><span data-stu-id="aaa20-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="aaa20-196">下面提供 hello 完整的指令碼供您參考</span><span class="sxs-lookup"><span data-stu-id="aaa20-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="aaa20-197">加入 hello 指令碼 toohello 復原計劃</span><span class="sxs-lookup"><span data-stu-id="aaa20-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="aaa20-198">Hello 指令碼準備就緒之後，您可以將它加入 toohello 您稍早建立的復原方案。</span><span class="sxs-lookup"><span data-stu-id="aaa20-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="aaa20-199">在您建立 hello 復原計劃，群組 2 之後指令碼選擇 tooadd。</span><span class="sxs-lookup"><span data-stu-id="aaa20-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="aaa20-200">指定指令碼名稱。</span><span class="sxs-lookup"><span data-stu-id="aaa20-200">Specify a script name.</span></span> <span data-ttu-id="aaa20-201">這是只顯示 hello 復原計劃中的此指令碼的好記名稱。</span><span class="sxs-lookup"><span data-stu-id="aaa20-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="aaa20-202">在 hello 容錯移轉 tooAzure 指令碼 – 選取 hello Azure 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="aaa20-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="aaa20-203">在 hello Azure Runbook，選取您所撰寫的 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="aaa20-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="aaa20-204">主要端指令碼</span><span class="sxs-lookup"><span data-stu-id="aaa20-204">Primary side scripts</span></span>
<span data-ttu-id="aaa20-205">當您執行容錯移轉 tooAzure 時，您也可以選擇 tooexecute 主要端指令碼。</span><span class="sxs-lookup"><span data-stu-id="aaa20-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="aaa20-206">這些指令碼會在容錯移轉期間 hello VMM 伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="aaa20-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="aaa20-207">主要端指令碼僅適用於關機前及關機後階段。</span><span class="sxs-lookup"><span data-stu-id="aaa20-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="aaa20-208">這是因為我們希望在 hello 主要站台 toobe 通常無法使用時所發生的災害事件。</span><span class="sxs-lookup"><span data-stu-id="aaa20-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="aaa20-209">期間發生未規劃的容錯移轉，只有當您選擇的主要站台作業，它會嘗試 toorun hello 主要端指令碼。</span><span class="sxs-lookup"><span data-stu-id="aaa20-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="aaa20-210">如果它們不是可連線，或逾時，將會繼續 hello 容錯移轉 toorecover hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aaa20-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="aaa20-211">未使用的 VMware/實體/hyper-v 站台不受保護的 VMM tooAzure-時容錯移轉 tooAzure 主要端指令碼。</span><span class="sxs-lookup"><span data-stu-id="aaa20-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="aaa20-212">不過，當您回復從 Azure tooon 內部部署主要端指令碼 (Runbook) 可以用於 VMware 以外的所有目標。</span><span class="sxs-lookup"><span data-stu-id="aaa20-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="aaa20-213">測試 hello 復原計劃</span><span class="sxs-lookup"><span data-stu-id="aaa20-213">Test hello recovery plan</span></span>
<span data-ttu-id="aaa20-214">一旦您加入 hello runbook toohello 計劃，您可以起始測試容錯移轉和觀看實作示範。</span><span class="sxs-lookup"><span data-stu-id="aaa20-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="aaa20-215">它一定會是建議的測試容錯移轉 tootest toorun 您應用程式和 hello 復原計劃 tooensure 沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="aaa20-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="aaa20-216">選取 hello 復原計劃，並起始測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="aaa20-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="aaa20-217">Hello 計劃在執行期間，您可以查看是否 hello runbook 已執行或不是透過其狀態。</span><span class="sxs-lookup"><span data-stu-id="aaa20-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="aaa20-218">您也可以查看 hello 詳細 hello runbook hello Azure 自動化作業 頁面上的 runbook 執行狀態。</span><span class="sxs-lookup"><span data-stu-id="aaa20-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="aaa20-219">Hello 容錯移轉完成時，除了 hello runbook 執行結果之後, 您可以查看 hello 執行是否成功或不是前往 hello Azure 的虛擬機器 頁面上，查看 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="aaa20-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="aaa20-220">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="aaa20-220">Sample scripts</span></span>
<span data-ttu-id="aaa20-221">雖然我們逐步進行作業自動化一個通常用在本教學課程中新增端點 tooan Azure 虛擬機器的工作，您可以執行其他使用 Azure 自動化的強大的自動化工作的數目。</span><span class="sxs-lookup"><span data-stu-id="aaa20-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="aaa20-222">Microsoft 與 hello Azure 自動化社群提供範例 runbook 可協助您開始建立您自己的方案和公用程式 runbook，您可以使用較大的自動化工作做為建置組塊。</span><span class="sxs-lookup"><span data-stu-id="aaa20-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="aaa20-223">開始使用它們從 hello 組件庫，並建置應用程式使用 Azure Site Recovery 強大的一種單鍵復原計劃。</span><span class="sxs-lookup"><span data-stu-id="aaa20-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aaa20-224">其他資源</span><span class="sxs-lookup"><span data-stu-id="aaa20-224">Additional Resources</span></span>
[<span data-ttu-id="aaa20-225">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="aaa20-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 自動化概觀")

[<span data-ttu-id="aaa20-226">Azure 自動化範例指令碼</span><span class="sxs-lookup"><span data-stu-id="aaa20-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 自動化範例指令碼")
