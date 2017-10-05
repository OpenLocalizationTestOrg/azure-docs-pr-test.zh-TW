---
title: "在傳統入口網站中將 Azure 自動化 Runbook 新增至復原方案 | Microsoft Docs"
description: "本文說明 Azure Site Recovery 現在讓您使用 Azure 自動化擴充復原計畫，以便在復原至 Azure 期間，完成複雜的工作"
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
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="d5898-103">在傳統入口網站中將 Azure 自動化 Runbook 新增至復原方案</span><span class="sxs-lookup"><span data-stu-id="d5898-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="d5898-104">本教學課程說明如何將 Azure Site Recovery 與 Azure 自動化整合在一起，以提供復原計畫的擴充性。</span><span class="sxs-lookup"><span data-stu-id="d5898-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="d5898-105">復原計畫可以協調使用 Azure Site Recovery 保護的虛擬機器復原，以便同時複寫至次要雲端和 Azure 案例。</span><span class="sxs-lookup"><span data-stu-id="d5898-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="d5898-106">復原方案也有助於讓復原「保持一致精確」、「可重複執行」及「自動化」。</span><span class="sxs-lookup"><span data-stu-id="d5898-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="d5898-107">如果您要將虛擬機器容錯移轉至 Azure，與 Azure 自動化整合可擴充復原計畫，並讓您能夠執行 Runbook，進而允許進行功能強大的自動化工作。</span><span class="sxs-lookup"><span data-stu-id="d5898-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="d5898-108">如果您還沒聽過「Azure 自動化」，請在[這裡](https://azure.microsoft.com/services/automation/)註冊，然後從[這裡](https://azure.microsoft.com/documentation/scripts/)下載其範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="d5898-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="d5898-109">使用[這裡](https://azure.microsoft.com/blog/?p=166264)的復原計劃進一步了解 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)，以及如何將復原協調至 Azure。</span><span class="sxs-lookup"><span data-stu-id="d5898-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="d5898-110">在本簡短教學課程中，我們將會探討如何將 Azure 自動化 Runbook 整合到復原計畫。</span><span class="sxs-lookup"><span data-stu-id="d5898-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="d5898-111">我們會將先前需要手動介入的簡單工作自動化，並了解如何將多步驟復原轉換成單鍵復原動作。</span><span class="sxs-lookup"><span data-stu-id="d5898-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="d5898-112">我們也將探討簡單的指令碼發生錯誤時如何進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="d5898-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="d5898-113">將應用程式保護到 Azure</span><span class="sxs-lookup"><span data-stu-id="d5898-113">Protect the application to Azure</span></span>
<span data-ttu-id="d5898-114">讓我們從兩部虛擬機器所組成的簡單應用程式開始。</span><span class="sxs-lookup"><span data-stu-id="d5898-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="d5898-115">在這裡，我們有 Fabrikam 的 HRweb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5898-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="d5898-116">Fabrikam-HRweb-frontend 和 Fabrikam-Hrweb-backend 是使用 Azure Site Recovery 保護到 Azure 的兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d5898-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="d5898-117">若要使用 Azure Site Recovery 保護虛擬機器，請遵循下列步驟進行。</span><span class="sxs-lookup"><span data-stu-id="d5898-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="d5898-118">對虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="d5898-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="d5898-119">請確定虛擬機器已經完成初始複寫，而且將要複寫。</span><span class="sxs-lookup"><span data-stu-id="d5898-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="d5898-120">請等到初始複寫完成，且複寫狀態變成 [受保護]。</span><span class="sxs-lookup"><span data-stu-id="d5898-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="d5898-121">在本教學課程中，我們將建立 Fabrikam HRweb 應用程式的復原計畫，以便將應用程式容錯移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="d5898-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="d5898-122">接著，我們會將它與將在容錯移轉的 Azure 虛擬機器上建立端點的 Runbook 整合，以便在連接埠 80 為網頁服務。</span><span class="sxs-lookup"><span data-stu-id="d5898-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="d5898-123">首先，讓我們為應用程式建立一個復原計畫。</span><span class="sxs-lookup"><span data-stu-id="d5898-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="d5898-124">建立復原計畫</span><span class="sxs-lookup"><span data-stu-id="d5898-124">Create the recovery plan</span></span>
<span data-ttu-id="d5898-125">若要將應用程式復原至 Azure，您必須建立一個復原計畫。</span><span class="sxs-lookup"><span data-stu-id="d5898-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="d5898-126">您可以使用復原計畫指定虛擬機器的復原順序。</span><span class="sxs-lookup"><span data-stu-id="d5898-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="d5898-127">放在群組 1 中的虛擬機器將會第一個復原並啟動，然後群組 2 中的虛擬機器將會接著進行。</span><span class="sxs-lookup"><span data-stu-id="d5898-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="d5898-128">建立一個如下的復原計畫。</span><span class="sxs-lookup"><span data-stu-id="d5898-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="d5898-129">若要深入了解復原計畫，請在 [這裡](https://msdn.microsoft.com/library/azure/dn788799.aspx "這裡")。</span><span class="sxs-lookup"><span data-stu-id="d5898-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="d5898-130">接下來，讓我們在 Azure 自動化中建立所需的構件。</span><span class="sxs-lookup"><span data-stu-id="d5898-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="d5898-131">建立自動化帳戶及其資產</span><span class="sxs-lookup"><span data-stu-id="d5898-131">Create the automation account and its assets</span></span>
<span data-ttu-id="d5898-132">您需要有 Azure 自動化帳戶才能建立 Runbook。</span><span class="sxs-lookup"><span data-stu-id="d5898-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="d5898-133">如果您還沒有帳戶，請瀏覽至以 ![](media/site-recovery-runbook-automation/02.png)表示的 [Azure 自動化] 索引標籤，然後建立一個新帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5898-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="d5898-134">為帳戶授與一個可識別的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5898-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="d5898-135">指定您要放置帳戶所在的地理區域。</span><span class="sxs-lookup"><span data-stu-id="d5898-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="d5898-136">建議您將帳戶放在與 ASR 保存庫相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="d5898-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="d5898-137">接下來，在帳戶中建立下列資產。</span><span class="sxs-lookup"><span data-stu-id="d5898-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="d5898-138">將訂用帳戶名稱新增為資產</span><span class="sxs-lookup"><span data-stu-id="d5898-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="d5898-139">在 Azure 自動化資產中加入新的設定 ![](media/site-recovery-runbook-automation/04.png)，然後選擇 ![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="d5898-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="d5898-140">將變數類型選取為 [字串] </span><span class="sxs-lookup"><span data-stu-id="d5898-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="d5898-141">將變數名稱指定為 **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="d5898-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="d5898-142">將您實際的 Azure 訂用帳戶名稱指定為變數值。</span><span class="sxs-lookup"><span data-stu-id="d5898-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="d5898-143">您可以從 Azure 入口網站上您帳戶的 [設定] 頁面識別您的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d5898-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="d5898-144">將 Azure 登入認證新增為資產</span><span class="sxs-lookup"><span data-stu-id="d5898-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="d5898-145">Azure 自動化使用 Azure PowerShell 連線到訂用帳戶，並在該處的構件上運作。</span><span class="sxs-lookup"><span data-stu-id="d5898-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="d5898-146">因此，您必須使用您的 Microsoft 帳戶或工作或學校帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d5898-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="d5898-147">您可以將帳戶認證儲存在 Runbook 可安全地使用的資產中。</span><span class="sxs-lookup"><span data-stu-id="d5898-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="d5898-148">在 Azure 自動化資產中加入新的設定 ![](media/site-recovery-runbook-automation/04.png)，然後選取 ![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="d5898-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="d5898-149">將 [認證類型] 選取為 [Windows PowerShell 認證] </span><span class="sxs-lookup"><span data-stu-id="d5898-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="d5898-150">將名稱指定為 **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="d5898-150">Specify the name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="d5898-151">指定用於登入的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d5898-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="d5898-152">現在，這兩個設定都可以在您的資產中使用。</span><span class="sxs-lookup"><span data-stu-id="d5898-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="d5898-153">[這裡](/powershell/azure/overview)提供有關如何透過 PowerShell 連線到您的訂用帳戶的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d5898-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="d5898-154">接下來，您將可以在 Azure 自動化中建立能夠在容錯移轉之後，為前端虛擬機器加入端點的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="d5898-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="d5898-155">Azure 自動化內容</span><span class="sxs-lookup"><span data-stu-id="d5898-155">Azure automation context</span></span>
<span data-ttu-id="d5898-156">ASR 將內容變數傳遞至 Runbook，以協助您撰寫具有決定性的指令碼。</span><span class="sxs-lookup"><span data-stu-id="d5898-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="d5898-157">其中一個雲端主張雲端服務和虛擬機器的名稱是可預測的，但有時候不一定可以預測，例如，當虛擬機器名稱可能因為在 Azure 中不支援某些字元而變更時。</span><span class="sxs-lookup"><span data-stu-id="d5898-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="d5898-158">因此，這項資訊會傳遞到 ASR 復原計畫，做為 *內容*的一部分。</span><span class="sxs-lookup"><span data-stu-id="d5898-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="d5898-159">以下是內容變數外觀的範例。</span><span class="sxs-lookup"><span data-stu-id="d5898-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="d5898-160">下表包含內容中每個變數的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="d5898-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="d5898-161">**變數名稱**</span><span class="sxs-lookup"><span data-stu-id="d5898-161">**Variable name**</span></span> | <span data-ttu-id="d5898-162">**說明**</span><span class="sxs-lookup"><span data-stu-id="d5898-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="d5898-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="d5898-163">RecoveryPlanName</span></span> |<span data-ttu-id="d5898-164">正在執行的計劃名稱。</span><span class="sxs-lookup"><span data-stu-id="d5898-164">Name of plan being run.</span></span> <span data-ttu-id="d5898-165">協助您根據名稱使用相同的指令碼採取動作</span><span class="sxs-lookup"><span data-stu-id="d5898-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="d5898-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="d5898-166">FailoverType</span></span> |<span data-ttu-id="d5898-167">指定容錯移轉是測試、已計劃，還是未計劃。</span><span class="sxs-lookup"><span data-stu-id="d5898-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="d5898-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="d5898-168">FailoverDirection</span></span> |<span data-ttu-id="d5898-169">指定復原是主要還是次要</span><span class="sxs-lookup"><span data-stu-id="d5898-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="d5898-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="d5898-170">GroupID</span></span> |<span data-ttu-id="d5898-171">識別計劃執行時復原計劃內的群組編號</span><span class="sxs-lookup"><span data-stu-id="d5898-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="d5898-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="d5898-172">VmMap</span></span> |<span data-ttu-id="d5898-173">群組中所有虛擬機器的陣列</span><span class="sxs-lookup"><span data-stu-id="d5898-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="d5898-174">VMMap 索引鍵</span><span class="sxs-lookup"><span data-stu-id="d5898-174">VMMap key</span></span> |<span data-ttu-id="d5898-175">每個 VM 的唯一索引鍵 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="d5898-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="d5898-176">與虛擬機器的適用 VMM ID 相同。</span><span class="sxs-lookup"><span data-stu-id="d5898-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="d5898-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="d5898-177">RoleName</span></span> |<span data-ttu-id="d5898-178">正在復原的 Azure VM 的名稱</span><span class="sxs-lookup"><span data-stu-id="d5898-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="d5898-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="d5898-179">CloudServiceName</span></span> |<span data-ttu-id="d5898-180">在其下建立虛擬機器的 Azure 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="d5898-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="d5898-181">若要識別內容中的 VmMap 索引鍵，您也可以移至 ASR 中的 [VM 屬性] 頁面，查看 VM GUID 屬性。</span><span class="sxs-lookup"><span data-stu-id="d5898-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="d5898-182">撰寫自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="d5898-182">Author an Automation runbook</span></span>
<span data-ttu-id="d5898-183">現在建立 Runbook，以開放前端虛擬機器上的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="d5898-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="d5898-184">在 Azure 自動化帳戶中，使用名稱 **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="d5898-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="d5898-185">瀏覽至 Runbook 的 [撰寫] 檢視，然後進入草稿模式。</span><span class="sxs-lookup"><span data-stu-id="d5898-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="d5898-186">首先，指定要當做復原計畫內容使用的變數</span><span class="sxs-lookup"><span data-stu-id="d5898-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="d5898-187">接下來，使用認證和訂用帳戶名稱，連線到訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d5898-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="d5898-188">請注意，您在這裡使用的是 Azure 的資產 – **AzureCredential** 和 **AzureSubscriptionName**。</span><span class="sxs-lookup"><span data-stu-id="d5898-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="d5898-189">現在，指定端點詳細資料以及您要公開端點所在虛擬機器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d5898-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="d5898-190">在這個案例中為前端虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d5898-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="d5898-191">這會指定 Azure 端點通訊協定、VM 上的本機連接埠及其對應的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="d5898-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="d5898-192">這些變數是將端點加入至 VM 的 Azure 命令所需的參數。</span><span class="sxs-lookup"><span data-stu-id="d5898-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="d5898-193">VMGUID 保留您操作所需的虛擬機器的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d5898-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="d5898-194">此指令碼現在會針對給定的 VM GUID 擷取內容，並在所參考的虛擬機器上建立端點。</span><span class="sxs-lookup"><span data-stu-id="d5898-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="d5898-195">這項操作完成之後，按 [發佈 ![](media/site-recovery-runbook-automation/20.png) ] 可讓您的指令碼可供執行。</span><span class="sxs-lookup"><span data-stu-id="d5898-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="d5898-196">以下提供完整的指令碼供您參考</span><span class="sxs-lookup"><span data-stu-id="d5898-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="d5898-197">將指令碼加入至復原計畫</span><span class="sxs-lookup"><span data-stu-id="d5898-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="d5898-198">一旦指令碼就緒之後，您就可以將它加入到您稍早建立的復原計畫。</span><span class="sxs-lookup"><span data-stu-id="d5898-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="d5898-199">在您建立的復原計畫中，選擇將指令碼加入到群組 2 後面。</span><span class="sxs-lookup"><span data-stu-id="d5898-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="d5898-200">指定指令碼名稱。</span><span class="sxs-lookup"><span data-stu-id="d5898-200">Specify a script name.</span></span> <span data-ttu-id="d5898-201">這只是此指令碼在復原計畫內用於顯示的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="d5898-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="d5898-202">在容錯移轉至 Azure 指令碼時 – 選取 Azure 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d5898-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="d5898-203">在 Azure Runbook 中，選取您所撰寫的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="d5898-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="d5898-204">主要端指令碼</span><span class="sxs-lookup"><span data-stu-id="d5898-204">Primary side scripts</span></span>
<span data-ttu-id="d5898-205">執行容錯移轉至 Azure 時，您也可以選擇執行主要端指令碼。</span><span class="sxs-lookup"><span data-stu-id="d5898-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="d5898-206">這些指令碼將在容錯移轉期間於 VMM 伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="d5898-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="d5898-207">主要端指令碼僅適用於關機前及關機後階段。</span><span class="sxs-lookup"><span data-stu-id="d5898-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="d5898-208">這是因為我們預期在發生災害事件時，通常無法使用主要網站。</span><span class="sxs-lookup"><span data-stu-id="d5898-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="d5898-209">在未規劃的容錯移轉期間，只有選擇主要網站作業時，才會嘗試執行主要端指令碼。</span><span class="sxs-lookup"><span data-stu-id="d5898-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="d5898-210">如果它們無法連線或逾時，則容錯移轉會繼續復原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d5898-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="d5898-211">容錯移轉至 Azure 時，若未針對 Azure 執行 VMM 保護，就無法為 VMware/實體/Hyper-v 網站使用主要端指令碼。</span><span class="sxs-lookup"><span data-stu-id="d5898-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="d5898-212">不過，當您從 Azure 容錯回復到內部部署時，主要端指令碼 (Runbooks) 可用於 VMware 以外的所有目標。</span><span class="sxs-lookup"><span data-stu-id="d5898-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="d5898-213">測試復原計畫</span><span class="sxs-lookup"><span data-stu-id="d5898-213">Test the recovery plan</span></span>
<span data-ttu-id="d5898-214">一旦您將 Runbook 加入至計畫之後，您可以起始一個測試容錯移轉，並觀看其運作。</span><span class="sxs-lookup"><span data-stu-id="d5898-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="d5898-215">建議您一律執行測試容錯移轉來測試您的應用程式與復原計畫，以確保沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="d5898-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="d5898-216">選取復原計畫，並起始測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d5898-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="d5898-217">在執行計劃期間，您可以透過其狀態查看 Runbook 是否已執行。</span><span class="sxs-lookup"><span data-stu-id="d5898-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="d5898-218">您也可以在 Runbook 的 [Azure 自動化工作] 頁面上查看詳細的 Runbook 執行狀態。</span><span class="sxs-lookup"><span data-stu-id="d5898-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="d5898-219">完成容錯移轉之後，除了 Runbook 執行結果之後，您還可以瀏覽 Azure 虛擬機器頁面並查看端點，以了解查看執行是否成功。</span><span class="sxs-lookup"><span data-stu-id="d5898-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="d5898-220">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="d5898-220">Sample scripts</span></span>
<span data-ttu-id="d5898-221">雖然我們在本教學課程中逐步說明如何將端點加入至 Azure 虛擬機器的其中一個常用工作自動化，但是您可以使用 Azure 自動化執行其他許多其他功能強大的自動化工作。</span><span class="sxs-lookup"><span data-stu-id="d5898-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="d5898-222">Microsoft 和 Azure 自動化社群會提供範例 Runbook，協助您開始建立自己的解決方案和公用程式 Runbook，而且您可以將這些 Runbook 做當大型自動化工作的建置組塊使用。</span><span class="sxs-lookup"><span data-stu-id="d5898-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="d5898-223">從資源庫開始使用這些 Runbook，並使用 Azure Site Recovery，為您的應用程式建置功能強大的單鍵復原計劃。</span><span class="sxs-lookup"><span data-stu-id="d5898-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5898-224">其他資源</span><span class="sxs-lookup"><span data-stu-id="d5898-224">Additional Resources</span></span>
[<span data-ttu-id="d5898-225">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="d5898-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 自動化概觀")

[<span data-ttu-id="d5898-226">Azure 自動化範例指令碼</span><span class="sxs-lookup"><span data-stu-id="d5898-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 自動化範例指令碼")
