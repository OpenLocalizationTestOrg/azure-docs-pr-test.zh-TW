---
title: "管理 Azure 自動化資料 | Microsoft Docs"
description: "本文章包含用於管理 Azure 自動化環境的多個主題。  目前將資料保留和備份 Azure 自動化災害復原併入 Azure 自動化中。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 92893edc4e02de148f6585e83c6861fd751401bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-automation-data"></a><span data-ttu-id="d0b87-104">管理 Azure 自動化資料</span><span class="sxs-lookup"><span data-stu-id="d0b87-104">Managing Azure Automation data</span></span>
<span data-ttu-id="d0b87-105">本文章包含用於管理 Azure 自動化環境的多個主題。</span><span class="sxs-lookup"><span data-stu-id="d0b87-105">This article contains multiple topics for managing an Azure Automation environment.</span></span>

## <a name="data-retention"></a><span data-ttu-id="d0b87-106">資料保留</span><span class="sxs-lookup"><span data-stu-id="d0b87-106">Data retention</span></span>
<span data-ttu-id="d0b87-107">當您刪除 Azure 自動化中的資源時，會將它保留 90 天作為稽核用途，之後才永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-107">When you delete a resource in Azure Automation, it is retained for 90 days for auditing purposes before being removed permanently.</span></span>  <span data-ttu-id="d0b87-108">在這段期間您無法看到或使用該資源。</span><span class="sxs-lookup"><span data-stu-id="d0b87-108">You can’t see or use the resource during this time.</span></span>  <span data-ttu-id="d0b87-109">此原則也適用於屬於已刪除的自動化帳戶的資源。</span><span class="sxs-lookup"><span data-stu-id="d0b87-109">This policy also applies to resources that belong to an automation account that is deleted.</span></span>

<span data-ttu-id="d0b87-110">Azure 自動化會自動刪除並永久移除超過 90 天的工作。</span><span class="sxs-lookup"><span data-stu-id="d0b87-110">Azure Automation automatically deletes and permanently removes jobs older than 90 days.</span></span>

<span data-ttu-id="d0b87-111">下表摘要說明不同的資源的保留原則。</span><span class="sxs-lookup"><span data-stu-id="d0b87-111">The following table summarizes the retention policy for different resources.</span></span>

| <span data-ttu-id="d0b87-112">資料</span><span class="sxs-lookup"><span data-stu-id="d0b87-112">Data</span></span> | <span data-ttu-id="d0b87-113">原則</span><span class="sxs-lookup"><span data-stu-id="d0b87-113">Policy</span></span> |
|:--- |:--- |
| <span data-ttu-id="d0b87-114">帳戶</span><span class="sxs-lookup"><span data-stu-id="d0b87-114">Accounts</span></span> |<span data-ttu-id="d0b87-115">刪除使用者帳戶 90 天後永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-115">Permanently removed 90 days after the account is deleted by a user.</span></span> |
| <span data-ttu-id="d0b87-116">Assets</span><span class="sxs-lookup"><span data-stu-id="d0b87-116">Assets</span></span> |<span data-ttu-id="d0b87-117">使用者刪除資產後 90 天，或使用者刪除持有資產的帳戶 90 天後永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-117">Permanently removed 90 days after the asset is deleted by a user, or 90 days after the account that holds the asset is deleted by a user.</span></span> |
| <span data-ttu-id="d0b87-118">模組</span><span class="sxs-lookup"><span data-stu-id="d0b87-118">Modules</span></span> |<span data-ttu-id="d0b87-119">使用者刪除模組後 90 天，或使用者刪除持有模組的帳戶 90 天後永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-119">Permanently removed 90 days after the module is deleted by a user, or 90 days after the account that holds the module is deleted by a user.</span></span> |
| <span data-ttu-id="d0b87-120">Runbook</span><span class="sxs-lookup"><span data-stu-id="d0b87-120">Runbooks</span></span> |<span data-ttu-id="d0b87-121">使用者刪除資源後 90 天，或使用者刪除持有資源的帳戶 90 天後永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-121">Permanently removed 90 days after the resource is deleted by a user, or 90 days after the account that holds the resource is deleted by a user.</span></span> |
| <span data-ttu-id="d0b87-122">作業</span><span class="sxs-lookup"><span data-stu-id="d0b87-122">Jobs</span></span> |<span data-ttu-id="d0b87-123">在上次修改日期的 90 天後刪除並永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-123">Deleted and permanently removed 90 days after last being modified.</span></span> <span data-ttu-id="d0b87-124">這可以是在工作完成、停止或暫止之後。</span><span class="sxs-lookup"><span data-stu-id="d0b87-124">This could be after the job completes, is stopped, or is suspended.</span></span> |
| <span data-ttu-id="d0b87-125">節點組態/MOF 檔案</span><span class="sxs-lookup"><span data-stu-id="d0b87-125">Node Configurations/MOF Files</span></span> |<span data-ttu-id="d0b87-126">舊的節點組態會在新的節點組態產生之後的 90 天永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-126">Old node configuration is permanently removed 90 days after a new node configuration is generated.</span></span> |
| <span data-ttu-id="d0b87-127">DSC 節點</span><span class="sxs-lookup"><span data-stu-id="d0b87-127">DSC Nodes</span></span> |<span data-ttu-id="d0b87-128">使用 Azure 入口網站或在 Windows PowerShell Cmdlet 中使用 [Unregister-AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) 在節點從自動化帳戶取消註冊之後的 90 天永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-128">Permanently removed 90 days after the node is unregistered from Automation Account using Azure portal or the [Unregister-AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) cmdlet in Windows PowerShell.</span></span> <span data-ttu-id="d0b87-129">節點也會在擁有節點的帳戶被使用者刪除之後的 90 天永久移除。</span><span class="sxs-lookup"><span data-stu-id="d0b87-129">Nodes are also permanently removed 90 days after the account that holds the node is deleted by a user.</span></span> |
| <span data-ttu-id="d0b87-130">節點報告</span><span class="sxs-lookup"><span data-stu-id="d0b87-130">Node Reports</span></span> |<span data-ttu-id="d0b87-131">該節點產生新的報告之後的 90 天永久移除</span><span class="sxs-lookup"><span data-stu-id="d0b87-131">Permanently removed 90 days after a new report is generated for that node</span></span> |

<span data-ttu-id="d0b87-132">保留原則適用於所有使用者，而且目前無法自訂。</span><span class="sxs-lookup"><span data-stu-id="d0b87-132">The retention policy applies to all users and currently cannot be customized.</span></span>

<span data-ttu-id="d0b87-133">不過，如果您需要將資料保留更長的時間，則可以將 Runbook 作業記錄轉送到 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="d0b87-133">However, if you need to retain data for a longer period of time, you can forward runbook job logs to Log Analytics.</span></span>  <span data-ttu-id="d0b87-134">如需進一步資訊，請檢閱[將 Azure 自動化作業資料轉送到 OMS Log Analytics](automation-manage-send-joblogs-log-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="d0b87-134">For further information, review [forward Azure Automation job data to OMS Log Analytics](automation-manage-send-joblogs-log-analytics.md).</span></span>   

## <a name="backing-up-azure-automation"></a><span data-ttu-id="d0b87-135">備份 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="d0b87-135">Backing up Azure Automation</span></span>
<span data-ttu-id="d0b87-136">在 Microsoft Azure 中刪除自動化帳戶時，會刪除帳戶中的所有物件，包括 Runbook、模組、組態、設定、工作和資產。</span><span class="sxs-lookup"><span data-stu-id="d0b87-136">When you delete an automation account in Microsoft Azure, all objects in the account are deleted including runbooks, modules, configurations, settings, jobs, and assets.</span></span> <span data-ttu-id="d0b87-137">刪除帳戶之後，就無法復原物件。</span><span class="sxs-lookup"><span data-stu-id="d0b87-137">The objects cannot be recovered after the account is deleted.</span></span>  <span data-ttu-id="d0b87-138">您可以使用下列資訊，在刪除之前備份您的自動化帳戶的內容。</span><span class="sxs-lookup"><span data-stu-id="d0b87-138">You can use the following information to backup the contents of your automation account before deleting it.</span></span> 

### <a name="runbooks"></a><span data-ttu-id="d0b87-139">Runbook</span><span class="sxs-lookup"><span data-stu-id="d0b87-139">Runbooks</span></span>
<span data-ttu-id="d0b87-140">您可以使用 Azure 管理入口網站或 Windows PowerShell 中的 [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) Cmdlet，將您的 Runbook 匯出為指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="d0b87-140">You can export your runbooks to script files using either the Azure Management Portal or the [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) cmdlet in Windows PowerShell.</span></span>  <span data-ttu-id="d0b87-141">可以將這些指令碼檔案匯入到另一個自動化帳戶，如 [建立或匯入 Runbook](https://msdn.microsoft.com/library/dn643637.aspx)中所述。</span><span class="sxs-lookup"><span data-stu-id="d0b87-141">These script files can be imported into another automation account as discussed in [Creating or Importing a Runbook](https://msdn.microsoft.com/library/dn643637.aspx).</span></span>

### <a name="integration-modules"></a><span data-ttu-id="d0b87-142">整合模組</span><span class="sxs-lookup"><span data-stu-id="d0b87-142">Integration modules</span></span>
<span data-ttu-id="d0b87-143">您無法從 Azure 自動化匯出整合模組。</span><span class="sxs-lookup"><span data-stu-id="d0b87-143">You cannot export integration modules from Azure Automation.</span></span>  <span data-ttu-id="d0b87-144">您必須確定它們可供在自動化帳戶外部使用。</span><span class="sxs-lookup"><span data-stu-id="d0b87-144">You must ensure that they are available outside of the automation account.</span></span>

### <a name="assets"></a><span data-ttu-id="d0b87-145">Assets</span><span class="sxs-lookup"><span data-stu-id="d0b87-145">Assets</span></span>
<span data-ttu-id="d0b87-146">您無法從 Azure 自動化匯出 [資產](https://msdn.microsoft.com/library/dn939988.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="d0b87-146">You cannot export [assets](https://msdn.microsoft.com/library/dn939988.aspx) from Azure Automation.</span></span>  <span data-ttu-id="d0b87-147">使用 Azure 管理入口網站，您必須記下變數、認證、憑證、連接和排程的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0b87-147">Using the Azure Management Portal, you must note the details of variables, credentials, certificates, connections, and schedules.</span></span>  <span data-ttu-id="d0b87-148">然後必須手動建立您匯入到另一個自動化的 Runbook 所使用的任何資產。</span><span class="sxs-lookup"><span data-stu-id="d0b87-148">You must then manually create any assets that are used by runbooks that you import into another automation.</span></span>

<span data-ttu-id="d0b87-149">您可以使用 [Azure Cmdlet](https://msdn.microsoft.com/library/dn690262.aspx) 來擷取未加密的資產的詳細資料並加以儲存供日後參考，或在另一個自動化帳戶中建立對等的資產。</span><span class="sxs-lookup"><span data-stu-id="d0b87-149">You can use [Azure cmdlets](https://msdn.microsoft.com/library/dn690262.aspx) to retrieve details of unencrypted assets and either save them for future reference or create equivalent assets in another automation account.</span></span>

<span data-ttu-id="d0b87-150">您無法使用 Cmdlet 擷取加密的變數的值或認證的密碼欄位。</span><span class="sxs-lookup"><span data-stu-id="d0b87-150">You cannot retrieve the value for encrypted variables or the password field of credentials using cmdlets.</span></span>  <span data-ttu-id="d0b87-151">如果您不知道這些值，則可從 Runbook 使用 [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) 和 [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) 活動來擷取它們。</span><span class="sxs-lookup"><span data-stu-id="d0b87-151">If you don't know these values, then you can retrieve them from a runbook using the [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) and [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) activities.</span></span>

<span data-ttu-id="d0b87-152">您無法從 Azure 自動化匯出憑證。</span><span class="sxs-lookup"><span data-stu-id="d0b87-152">You cannot export certificates from Azure Automation.</span></span>  <span data-ttu-id="d0b87-153">您必須確定 Azure 外部有任何憑證可供使用。</span><span class="sxs-lookup"><span data-stu-id="d0b87-153">You must ensure that any certificates are available outside of Azure.</span></span>

### <a name="dsc-configurations"></a><span data-ttu-id="d0b87-154">DSC 組態</span><span class="sxs-lookup"><span data-stu-id="d0b87-154">DSC configurations</span></span>
<span data-ttu-id="d0b87-155">您可以使用 Azure 管理入口網站或 Windows PowerShell 中的 [Export-AzureRmAutomationDscConfiguration](https://msdn.microsoft.com/library/mt603485.aspx) Cmdlet，將您的組態匯出為指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="d0b87-155">You can export your configurations to script files using either the Azure Management Portal or the [Export-AzureRmAutomationDscConfiguration](https://msdn.microsoft.com/library/mt603485.aspx) cmdlet in Windows PowerShell.</span></span> <span data-ttu-id="d0b87-156">這些組態可以匯入並用於另一個自動化帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d0b87-156">These configurations can be imported and used in another automation account.</span></span>

## <a name="geo-replication-in-azure-automation"></a><span data-ttu-id="d0b87-157">Azure 自動化中的異地複寫</span><span class="sxs-lookup"><span data-stu-id="d0b87-157">Geo-replication in Azure Automation</span></span>
<span data-ttu-id="d0b87-158">異地複寫是 Azure 自動化帳戶中的標準功能，可將帳戶資料備份到其他地理區域做為備援。</span><span class="sxs-lookup"><span data-stu-id="d0b87-158">Geo-replication, standard in Azure Automation accounts, backs up account data to a different geographical region for redundancy.</span></span> <span data-ttu-id="d0b87-159">您可以在設定帳戶時選擇主要區域，然後就會自動指派次要區域給帳戶。</span><span class="sxs-lookup"><span data-stu-id="d0b87-159">You can choose a primary region when setting up your account, and then a secondary region is assigned to it automatically.</span></span> <span data-ttu-id="d0b87-160">從主要區域複製到次要區域的資料會持續更新，以防止資料遺失。</span><span class="sxs-lookup"><span data-stu-id="d0b87-160">The secondary data, copied from the primary region, is continuously updated in case of data loss.</span></span>  

<span data-ttu-id="d0b87-161">下表顯示可用的主要和次要區域配對：</span><span class="sxs-lookup"><span data-stu-id="d0b87-161">The following table shows the available primary and secondary region pairings.</span></span>

| <span data-ttu-id="d0b87-162">主要</span><span class="sxs-lookup"><span data-stu-id="d0b87-162">Primary</span></span> | <span data-ttu-id="d0b87-163">次要</span><span class="sxs-lookup"><span data-stu-id="d0b87-163">Secondary</span></span> |
| --- | --- |
| <span data-ttu-id="d0b87-164">美國中南部</span><span class="sxs-lookup"><span data-stu-id="d0b87-164">South Central US</span></span> |<span data-ttu-id="d0b87-165">美國中北部</span><span class="sxs-lookup"><span data-stu-id="d0b87-165">North Central US</span></span> |
| <span data-ttu-id="d0b87-166">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="d0b87-166">US East 2</span></span> |<span data-ttu-id="d0b87-167">美國中部</span><span class="sxs-lookup"><span data-stu-id="d0b87-167">Central US</span></span> |
| <span data-ttu-id="d0b87-168">西歐</span><span class="sxs-lookup"><span data-stu-id="d0b87-168">West Europe</span></span> |<span data-ttu-id="d0b87-169">北歐</span><span class="sxs-lookup"><span data-stu-id="d0b87-169">North Europe</span></span> |
| <span data-ttu-id="d0b87-170">東南亞</span><span class="sxs-lookup"><span data-stu-id="d0b87-170">South East Asia</span></span> |<span data-ttu-id="d0b87-171">東亞</span><span class="sxs-lookup"><span data-stu-id="d0b87-171">East Asia</span></span> |
| <span data-ttu-id="d0b87-172">日本東部</span><span class="sxs-lookup"><span data-stu-id="d0b87-172">Japan East</span></span> |<span data-ttu-id="d0b87-173">日本西部</span><span class="sxs-lookup"><span data-stu-id="d0b87-173">Japan West</span></span> |

<span data-ttu-id="d0b87-174">萬一主區域資料遺失，Microsoft 會嘗試將它復原。</span><span class="sxs-lookup"><span data-stu-id="d0b87-174">In the unlikely event that a primary region data is lost, Microsoft attempts to recover it.</span></span> <span data-ttu-id="d0b87-175">如果主要資料無法復原，則會執行異地容錯移轉，而且將透過受影響客戶的訂用帳戶將此情況通知他們。</span><span class="sxs-lookup"><span data-stu-id="d0b87-175">If the primary data cannot be recovered, then geo-failover is performed and the affected customers will be notified about this through their subscription.</span></span>

