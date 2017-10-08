---
title: "在 Azure 自動化中的 aaaRole 型存取控制 |Microsoft 文件"
description: "角色型存取控制 (RBAC) 可以啟用對 Azure 資源的存取權管理。 本文說明如何在 Azure 自動化中的 RBAC 的向上 tooset。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "自動化 rbac, 角色型存取控制, azure rbac"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a><span data-ttu-id="0ac29-105">Azure 自動化中的角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="0ac29-105">Role-based access control in Azure Automation</span></span>
## <a name="role-based-access-control"></a><span data-ttu-id="0ac29-106">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="0ac29-106">Role-based access control</span></span>
<span data-ttu-id="0ac29-107">角色型存取控制 (RBAC) 可以啟用對 Azure 資源的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="0ac29-107">Role-based access control (RBAC) enables access management for Azure resources.</span></span> <span data-ttu-id="0ac29-108">使用[RBAC](../active-directory/role-based-access-control-configure.md)、 您可以在您的小組隔離責任和授與僅 hello 存取 toousers、 群組和應用程式，它們必須 tooperform 他們的工作數量。</span><span class="sxs-lookup"><span data-stu-id="0ac29-108">Using [RBAC](../active-directory/role-based-access-control-configure.md), you can segregate duties within your team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span> <span data-ttu-id="0ac29-109">可以授與以角色為基礎的存取權 toousers 使用 hello Azure 入口網站、 Azure 命令列工具或 Azure 管理 Api。</span><span class="sxs-lookup"><span data-stu-id="0ac29-109">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

## <a name="rbac-in-automation-accounts"></a><span data-ttu-id="0ac29-110">自動化帳戶中的 RBAC</span><span class="sxs-lookup"><span data-stu-id="0ac29-110">RBAC in Automation Accounts</span></span>
<span data-ttu-id="0ac29-111">在 Azure 自動化中，會授與存取指派適當 RBAC 角色 toousers hello、 群組和應用程式在 hello 自動化帳戶範圍。</span><span class="sxs-lookup"><span data-stu-id="0ac29-111">In Azure Automation, access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at hello Automation account scope.</span></span> <span data-ttu-id="0ac29-112">下列是 hello 支援自動化帳戶的內建角色：</span><span class="sxs-lookup"><span data-stu-id="0ac29-112">Following are hello built-in roles supported by an Automation account:</span></span>  

| <span data-ttu-id="0ac29-113">**角色**</span><span class="sxs-lookup"><span data-stu-id="0ac29-113">**Role**</span></span> | <span data-ttu-id="0ac29-114">**說明**</span><span class="sxs-lookup"><span data-stu-id="0ac29-114">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ac29-115">擁有者</span><span class="sxs-lookup"><span data-stu-id="0ac29-115">Owner</span></span> |<span data-ttu-id="0ac29-116">hello 擁有者角色允許存取 tooall 資源，以及包括提供存取 tooother 使用者、 群組和應用程式 toomanage hello 自動化帳戶的自動化帳戶內的動作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-116">hello Owner role allows access tooall resources and actions within an Automation account including providing access tooother users, groups and applications toomanage hello Automation account.</span></span> |
| <span data-ttu-id="0ac29-117">參與者</span><span class="sxs-lookup"><span data-stu-id="0ac29-117">Contributor</span></span> |<span data-ttu-id="0ac29-118">hello 參與者角色可讓您 toomanage 以外修改其他使用者的所有內容存取權限 tooan 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ac29-118">hello Contributor role allows you toomanage everything except modifying other user’s access permissions tooan Automation account.</span></span> |
| <span data-ttu-id="0ac29-119">讀取者</span><span class="sxs-lookup"><span data-stu-id="0ac29-119">Reader</span></span> |<span data-ttu-id="0ac29-120">hello 讀取者角色可讓您 tooview 自動化中的所有 hello 資源帳戶，但無法進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="0ac29-120">hello Reader role allows you tooview all hello resources in an Automation account but cannot make any changes.</span></span> |
| <span data-ttu-id="0ac29-121">自動化運算子</span><span class="sxs-lookup"><span data-stu-id="0ac29-121">Automation Operator</span></span> |<span data-ttu-id="0ac29-122">hello 自動化操作員角色可讓您 tooperform 操作工作例如啟動、 停止、 暫停、 繼續和排程作業。</span><span class="sxs-lookup"><span data-stu-id="0ac29-122">hello Automation Operator role allows you tooperform operational tasks such as start, stop, suspend, resume and schedule jobs.</span></span> <span data-ttu-id="0ac29-123">這個角色是如果您想要 tooprotect 您的自動化帳戶資源，例如認證資產和 runbook 進行檢視或修改很有幫助，但是仍然允許這些 runbook 的組織 tooexecute 成員。</span><span class="sxs-lookup"><span data-stu-id="0ac29-123">This role is helpful if you want tooprotect your Automation Account resources like credentials assets and runbooks from being viewed or modified but still allow members of your organization tooexecute these runbooks.</span></span> |
| <span data-ttu-id="0ac29-124">使用者存取系統管理員</span><span class="sxs-lookup"><span data-stu-id="0ac29-124">User Access Administrator</span></span> |<span data-ttu-id="0ac29-125">hello 使用者存取系統管理員角色，可讓您 toomanage 使用者存取 tooAzure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ac29-125">hello User Access Administrator role allows you toomanage user access tooAzure Automation accounts.</span></span> |

> [!NOTE]
> <span data-ttu-id="0ac29-126">您無法授與存取權限 tooa 特定 runbook 或 runbook，只 toohello 資源，以及在 hello 自動化帳戶內的動作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-126">You cannot grant access rights tooa specific runbook or runbooks, only toohello resources and actions within hello Automation account.</span></span>  
> 
> 

<span data-ttu-id="0ac29-127">本文章中我們將逐步引導您在 Azure 自動化中的 RBAC 的向上 tooset。</span><span class="sxs-lookup"><span data-stu-id="0ac29-127">In this article we will walk you through how tooset up RBAC in Azure Automation.</span></span> <span data-ttu-id="0ac29-128">但首先，讓我們來看得更仔細查看 hello 個別權限授與 toohello 參與者，讀取器、 自動化運算子和使用者存取系統管理員，讓我們取得之前授與任何人都了解 rights toohello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ac29-128">But first, let's take a closer look at hello individual permissions granted toohello Contributor, Reader, Automation Operator and User Access Administrator so that we gain a good understanding before granting anyone rights toohello Automation account.</span></span>  <span data-ttu-id="0ac29-129">否則，可能會造成非預期或不想要的結果。</span><span class="sxs-lookup"><span data-stu-id="0ac29-129">Otherwise it could result in unintended or undesirable consequences.</span></span>     

## <a name="contributor-role-permissions"></a><span data-ttu-id="0ac29-130">參與者角色權限</span><span class="sxs-lookup"><span data-stu-id="0ac29-130">Contributor role permissions</span></span>
<span data-ttu-id="0ac29-131">hello 下表顯示 hello 自動化中的 hello 參與者角色可以執行的特定動作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-131">hello following table presents hello specific actions that can be performed by hello Contributor role in Automation.</span></span>

| <span data-ttu-id="0ac29-132">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="0ac29-132">**Resource Type**</span></span> | <span data-ttu-id="0ac29-133">**讀取**</span><span class="sxs-lookup"><span data-stu-id="0ac29-133">**Read**</span></span> | <span data-ttu-id="0ac29-134">**寫入**</span><span class="sxs-lookup"><span data-stu-id="0ac29-134">**Write**</span></span> | <span data-ttu-id="0ac29-135">**刪除**</span><span class="sxs-lookup"><span data-stu-id="0ac29-135">**Delete**</span></span> | <span data-ttu-id="0ac29-136">**其他動作**</span><span class="sxs-lookup"><span data-stu-id="0ac29-136">**Other Actions**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0ac29-137">Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="0ac29-137">Azure Automation Account</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-141">自動化憑證資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-141">Automation Certificate Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-145">自動化連線資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-145">Automation Connection Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-149">自動化連線類型資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-149">Automation Connection Type Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-153">自動化認證資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-153">Automation Credential Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-157">自動化排程資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-157">Automation Schedule Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-161">自動化變數資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-161">Automation Variable Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-165">自動化期望狀態組態</span><span class="sxs-lookup"><span data-stu-id="0ac29-165">Automation Desired State Configuration</span></span> | | | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="0ac29-167">Hybrid Runbook Worker 類型</span><span class="sxs-lookup"><span data-stu-id="0ac29-167">Hybrid Runbook Worker Resource Type</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-170">Azure 自動化作業</span><span class="sxs-lookup"><span data-stu-id="0ac29-170">Azure Automation Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="0ac29-174">自動化作業串流</span><span class="sxs-lookup"><span data-stu-id="0ac29-174">Automation Job Stream</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-176">自動化作業排程</span><span class="sxs-lookup"><span data-stu-id="0ac29-176">Automation Job Schedule</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-180">自動化模組</span><span class="sxs-lookup"><span data-stu-id="0ac29-180">Automation Module</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="0ac29-184">Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="0ac29-184">Azure Automation Runbook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="0ac29-189">自動化 Runbook 草稿</span><span class="sxs-lookup"><span data-stu-id="0ac29-189">Automation Runbook Draft</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="0ac29-192">自動化 Runbook 草稿測試作業</span><span class="sxs-lookup"><span data-stu-id="0ac29-192">Automation Runbook Draft Test Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="0ac29-196">自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="0ac29-196">Automation Webhook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a><span data-ttu-id="0ac29-201">讀取者角色權限</span><span class="sxs-lookup"><span data-stu-id="0ac29-201">Reader role permissions</span></span>
<span data-ttu-id="0ac29-202">hello 下表顯示 hello 可以在自動化中的 hello 讀取器角色所執行的特定動作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-202">hello following table presents hello specific actions that can be performed by hello Reader role in Automation.</span></span>

| <span data-ttu-id="0ac29-203">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="0ac29-203">**Resource Type**</span></span> | <span data-ttu-id="0ac29-204">**讀取**</span><span class="sxs-lookup"><span data-stu-id="0ac29-204">**Read**</span></span> | <span data-ttu-id="0ac29-205">**寫入**</span><span class="sxs-lookup"><span data-stu-id="0ac29-205">**Write**</span></span> | <span data-ttu-id="0ac29-206">**刪除**</span><span class="sxs-lookup"><span data-stu-id="0ac29-206">**Delete**</span></span> | <span data-ttu-id="0ac29-207">**其他動作**</span><span class="sxs-lookup"><span data-stu-id="0ac29-207">**Other Actions**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0ac29-208">傳統訂用帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="0ac29-208">Classic subscription administrator</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-210">管理鎖定</span><span class="sxs-lookup"><span data-stu-id="0ac29-210">Management lock</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-212">權限</span><span class="sxs-lookup"><span data-stu-id="0ac29-212">Permission</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-214">提供者作業</span><span class="sxs-lookup"><span data-stu-id="0ac29-214">Provider operations</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-216">角色指派</span><span class="sxs-lookup"><span data-stu-id="0ac29-216">Role assignment</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-218">角色定義</span><span class="sxs-lookup"><span data-stu-id="0ac29-218">Role definition</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a><span data-ttu-id="0ac29-220">自動化操作員角色權限</span><span class="sxs-lookup"><span data-stu-id="0ac29-220">Automation Operator role permissions</span></span>
<span data-ttu-id="0ac29-221">hello 下表顯示 hello 可執行的自動化中的 hello 自動化操作員角色的特定動作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-221">hello following table presents hello specific actions that can be performed by hello Automation Operator role in Automation.</span></span>

| <span data-ttu-id="0ac29-222">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="0ac29-222">**Resource Type**</span></span> | <span data-ttu-id="0ac29-223">**讀取**</span><span class="sxs-lookup"><span data-stu-id="0ac29-223">**Read**</span></span> | <span data-ttu-id="0ac29-224">**寫入**</span><span class="sxs-lookup"><span data-stu-id="0ac29-224">**Write**</span></span> | <span data-ttu-id="0ac29-225">**刪除**</span><span class="sxs-lookup"><span data-stu-id="0ac29-225">**Delete**</span></span> | <span data-ttu-id="0ac29-226">**其他動作**</span><span class="sxs-lookup"><span data-stu-id="0ac29-226">**Other Actions**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0ac29-227">Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="0ac29-227">Azure Automation Account</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-229">自動化憑證資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-229">Automation Certificate Asset</span></span> | | | | |
| <span data-ttu-id="0ac29-230">自動化連線資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-230">Automation Connection Asset</span></span> | | | | |
| <span data-ttu-id="0ac29-231">自動化連線類型資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-231">Automation Connection Type Asset</span></span> | | | | |
| <span data-ttu-id="0ac29-232">自動化認證資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-232">Automation Credential Asset</span></span> | | | | |
| <span data-ttu-id="0ac29-233">自動化排程資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-233">Automation Schedule Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |
| <span data-ttu-id="0ac29-236">自動化變數資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-236">Automation Variable Asset</span></span> | | | | |
| <span data-ttu-id="0ac29-237">自動化期望狀態組態</span><span class="sxs-lookup"><span data-stu-id="0ac29-237">Automation Desired State Configuration</span></span> | | | | |
| <span data-ttu-id="0ac29-238">Hybrid Runbook Worker 類型</span><span class="sxs-lookup"><span data-stu-id="0ac29-238">Hybrid Runbook Worker Resource Type</span></span> | | | | |
| <span data-ttu-id="0ac29-239">Azure 自動化作業</span><span class="sxs-lookup"><span data-stu-id="0ac29-239">Azure Automation Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="0ac29-243">自動化作業串流</span><span class="sxs-lookup"><span data-stu-id="0ac29-243">Automation Job Stream</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-245">自動化作業排程</span><span class="sxs-lookup"><span data-stu-id="0ac29-245">Automation Job Schedule</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |
| <span data-ttu-id="0ac29-248">自動化模組</span><span class="sxs-lookup"><span data-stu-id="0ac29-248">Automation Module</span></span> | | | | |
| <span data-ttu-id="0ac29-249">Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="0ac29-249">Azure Automation Runbook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-251">自動化 Runbook 草稿</span><span class="sxs-lookup"><span data-stu-id="0ac29-251">Automation Runbook Draft</span></span> | | | | |
| <span data-ttu-id="0ac29-252">自動化 Runbook 草稿測試作業</span><span class="sxs-lookup"><span data-stu-id="0ac29-252">Automation Runbook Draft Test Job</span></span> | | | | |
| <span data-ttu-id="0ac29-253">自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="0ac29-253">Automation Webhook</span></span> | | | | |

<span data-ttu-id="0ac29-254">如需詳細資訊，hello[自動化運算子動作](../active-directory/role-based-access-built-in-roles.md#automation-operator)清單 hello hello 自動化帳戶和其資源的 hello 自動化操作員角色所支援的動作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-254">For further details, hello [Automation operator actions](../active-directory/role-based-access-built-in-roles.md#automation-operator) lists hello actions supported by hello Automation operator role on hello Automation account and its resources.</span></span>

## <a name="user-access-administrator-role-permissions"></a><span data-ttu-id="0ac29-255">使用者存取系統管理員角色權限</span><span class="sxs-lookup"><span data-stu-id="0ac29-255">User Access Administrator role permissions</span></span>
<span data-ttu-id="0ac29-256">hello 下表顯示 hello hello 自動化中的使用者存取系統管理員角色可以執行的特定動作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-256">hello following table presents hello specific actions that can be performed by hello User Access Administrator role in Automation.</span></span>

| <span data-ttu-id="0ac29-257">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="0ac29-257">**Resource Type**</span></span> | <span data-ttu-id="0ac29-258">**讀取**</span><span class="sxs-lookup"><span data-stu-id="0ac29-258">**Read**</span></span> | <span data-ttu-id="0ac29-259">**寫入**</span><span class="sxs-lookup"><span data-stu-id="0ac29-259">**Write**</span></span> | <span data-ttu-id="0ac29-260">**刪除**</span><span class="sxs-lookup"><span data-stu-id="0ac29-260">**Delete**</span></span> | <span data-ttu-id="0ac29-261">**其他動作**</span><span class="sxs-lookup"><span data-stu-id="0ac29-261">**Other Actions**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0ac29-262">Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="0ac29-262">Azure Automation Account</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-264">自動化憑證資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-264">Automation Certificate Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-266">自動化連線資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-266">Automation Connection Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-268">自動化連線類型資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-268">Automation Connection Type Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-270">自動化認證資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-270">Automation Credential Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-272">自動化排程資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-272">Automation Schedule Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-274">自動化變數資產</span><span class="sxs-lookup"><span data-stu-id="0ac29-274">Automation Variable Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-276">自動化期望狀態組態</span><span class="sxs-lookup"><span data-stu-id="0ac29-276">Automation Desired State Configuration</span></span> | | | | |
| <span data-ttu-id="0ac29-277">Hybrid Runbook Worker 類型</span><span class="sxs-lookup"><span data-stu-id="0ac29-277">Hybrid Runbook Worker Resource Type</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-279">Azure 自動化作業</span><span class="sxs-lookup"><span data-stu-id="0ac29-279">Azure Automation Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-281">自動化作業串流</span><span class="sxs-lookup"><span data-stu-id="0ac29-281">Automation Job Stream</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-283">自動化作業排程</span><span class="sxs-lookup"><span data-stu-id="0ac29-283">Automation Job Schedule</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-285">自動化模組</span><span class="sxs-lookup"><span data-stu-id="0ac29-285">Automation Module</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-287">Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="0ac29-287">Azure Automation Runbook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-289">自動化 Runbook 草稿</span><span class="sxs-lookup"><span data-stu-id="0ac29-289">Automation Runbook Draft</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-291">自動化 Runbook 草稿測試作業</span><span class="sxs-lookup"><span data-stu-id="0ac29-291">Automation Runbook Draft Test Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="0ac29-293">自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="0ac29-293">Automation Webhook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a><span data-ttu-id="0ac29-295">使用 Azure 入口網站為您的自動化帳戶設定 RBAC</span><span class="sxs-lookup"><span data-stu-id="0ac29-295">Configure RBAC for your Automation Account using Azure Portal</span></span>
1. <span data-ttu-id="0ac29-296">登入 toohello [Azure 入口網站](https://portal.azure.com/)從 hello 自動化帳戶 刀鋒視窗中開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ac29-296">Log in toohello [Azure Portal](https://portal.azure.com/) and open your Automation account from hello Automation Accounts blade.</span></span>  
2. <span data-ttu-id="0ac29-297">按一下 hello**存取**頂端 hello 右下角的控制項。</span><span class="sxs-lookup"><span data-stu-id="0ac29-297">Click on hello **Access** control at hello top right corner.</span></span> <span data-ttu-id="0ac29-298">這會開啟 hello**使用者**刀鋒視窗可以讓您加入新的使用者、 群組和應用程式 toomanage 自動化帳戶，然後檢視現有的角色，可設定為 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ac29-298">This opens hello **Users** blade where you can add new users, groups and applications toomanage your Automation account and view existing roles that can be configured for hello Automation Account.</span></span>  
   
   ![[存取] 按鈕](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> <span data-ttu-id="0ac29-300">**訂用帳戶系統管理員 」** hello 預設使用者為已經存在。</span><span class="sxs-lookup"><span data-stu-id="0ac29-300">**Subscription admins** already exists as hello default user.</span></span> <span data-ttu-id="0ac29-301">hello 訂用帳戶系統管理員 」 的 active directory 群組包含 hello 服務給系統管理員和 co-administrator(s) Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ac29-301">hello subscription admins active directory group includes hello service administrator(s) and co-administrator(s) for your Azure subscription.</span></span> <span data-ttu-id="0ac29-302">hello 服務管理員是 hello 的擁有者 Azure 訂用帳戶以及它的資源，而且會有 hello 擁有者角色繼承 hello 自動化帳戶太。</span><span class="sxs-lookup"><span data-stu-id="0ac29-302">hello Service admin is hello owner of your Azure subscription and its resources, and will have hello owner role inherited for hello automation accounts too.</span></span> <span data-ttu-id="0ac29-303">這表示 hello 存取**繼承**如**服務系統管理員和共同管理員**的訂用帳戶和它的**指派**針對所有 hello 其他使用者。</span><span class="sxs-lookup"><span data-stu-id="0ac29-303">This means that hello access is **Inherited** for **service administrators and co-admins** of a subscription and it’s **Assigned** for all hello other users.</span></span> <span data-ttu-id="0ac29-304">按一下**訂閱管理員**tooview 更詳細說明有關其權限。</span><span class="sxs-lookup"><span data-stu-id="0ac29-304">Click **Subscription admins** tooview more details about their permissions.</span></span>  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a><span data-ttu-id="0ac29-305">加入新使用者並指派角色</span><span class="sxs-lookup"><span data-stu-id="0ac29-305">Add a new user and assign a role</span></span>
1. <span data-ttu-id="0ac29-306">從 hello 使用者 刀鋒視窗中，按一下 **新增**tooopen hello**新增存取 刀鋒視窗**您可以在其中新增使用者、 群組或應用程式，並指派角色 toothem。</span><span class="sxs-lookup"><span data-stu-id="0ac29-306">From hello Users blade, click **Add** tooopen hello **Add access blade** where you can add a user, group, or application, and assign a role toothem.</span></span>  
   
   ![新增使用者](media/automation-role-based-access-control/automation-02-add-user.png)  
2. <span data-ttu-id="0ac29-308">從可用角色的 hello 清單中選取的角色。</span><span class="sxs-lookup"><span data-stu-id="0ac29-308">Select a role from hello list of available roles.</span></span> <span data-ttu-id="0ac29-309">我們將選擇 hello**讀取器**角色，但是您可以選擇任何 hello 可用的內建角色支援自動化帳戶或您已定義任何自訂角色。</span><span class="sxs-lookup"><span data-stu-id="0ac29-309">We will choose hello **Reader** role, but you can choose any of hello available built-in roles that an Automation Account supports or any custom role you may have defined.</span></span>  
   
   ![選取角色](media/automation-role-based-access-control/automation-03-select-role.png)  
3. <span data-ttu-id="0ac29-311">按一下**將使用者新增**tooopen hello**將使用者新增**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0ac29-311">Click on **Add users** tooopen hello **Add users** blade.</span></span> <span data-ttu-id="0ac29-312">如果您新增任何使用者、 群組或應用程式 toomanage 列出您的訂用帳戶則這些使用者，並選取 tooadd 存取。</span><span class="sxs-lookup"><span data-stu-id="0ac29-312">If you have added any users, groups, or applications toomanage your subscription then those users are listed and you can select them tooadd access.</span></span> <span data-ttu-id="0ac29-313">如果沒有列出任何使用者，或如果未列出您感興趣加入 hello 使用者再按一下**邀請**tooopen hello**邀請來賓**刀鋒視窗中，您可以在此邀請具有有效的 Microsoft 帳戶的使用者電子郵件地址，例如 Outlook.com、 OneDrive 或 Xbox Live Id。</span><span class="sxs-lookup"><span data-stu-id="0ac29-313">If there aren’t any users listed, or if hello user you are interested in adding is not listed then click **invite** tooopen hello **Invite a guest** blade, where you can invite a user with a valid Microsoft account email address such as Outlook.com, OneDrive, or Xbox Live Ids.</span></span> <span data-ttu-id="0ac29-314">一旦您已輸入 hello hello 使用者電子郵件地址，按一下 **選取**tooadd hello 使用者，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="0ac29-314">Once you have entered hello email address of hello user, click **Select** tooadd hello user, and then click **OK**.</span></span> 
   
   ![新增使用者](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   <span data-ttu-id="0ac29-316">現在您應該會看到新增的 hello 使用者 toohello**使用者**刀鋒視窗的 hello**讀取器**指派角色。</span><span class="sxs-lookup"><span data-stu-id="0ac29-316">Now you should see hello user added toohello **Users** blade with hello **Reader** role assigned.</span></span>  
   
   ![列出使用者](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   <span data-ttu-id="0ac29-318">您也可以指派角色 toohello 使用者從 hello**角色**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0ac29-318">You can also assign a role toohello user from hello **Roles** blade.</span></span> 
4. <span data-ttu-id="0ac29-319">按一下**角色**從 hello 使用者 刀鋒視窗 tooopen hello**角色 刀鋒視窗**。</span><span class="sxs-lookup"><span data-stu-id="0ac29-319">Click **Roles** from hello Users blade tooopen hello **Roles blade**.</span></span> <span data-ttu-id="0ac29-320">您可以從這個刀鋒視窗中，檢視 hello hello 角色，hello 數目的使用者和群組指派 toothat 角色名稱。</span><span class="sxs-lookup"><span data-stu-id="0ac29-320">From this blade, you can view hello name of hello role, hello number of users and groups assigned toothat role.</span></span>
   
    ![從 [使用者] 刀鋒視窗指派角色](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > <span data-ttu-id="0ac29-322">以角色為基礎的存取控制只可以在 hello 自動化帳戶層級設定，並不是在下列任何資源 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ac29-322">Role-based access control can only be set at hello Automation Account level and not at any resource below hello Automation Account.</span></span>
   > 
   > 
   
    <span data-ttu-id="0ac29-323">您可以指派多個角色 tooa 使用者、 群組或應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ac29-323">You can assign more than one role tooa user, group, or application.</span></span> <span data-ttu-id="0ac29-324">例如，如果我們加入 hello**自動化運算子**角色以及 hello**讀取者角色**toohello 使用者，然後他們可以檢視所有 hello 自動化資源，以及執行 hello runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-324">For example, if we add hello **Automation Operator** role along with hello **Reader role** toohello user, then they can view all hello Automation resources, as well as execute hello runbook jobs.</span></span> <span data-ttu-id="0ac29-325">您可以展開 hello 下拉式 tooview 的角色指派 toohello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="0ac29-325">You can expand hello dropdown tooview a list of roles assigned toohello user.</span></span>  
   
    ![檢視多個角色](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a><span data-ttu-id="0ac29-327">移除使用者</span><span class="sxs-lookup"><span data-stu-id="0ac29-327">Remove a user</span></span>
<span data-ttu-id="0ac29-328">您可以移除 hello 人員不管理 hello 自動化帳戶或使用者不再適用於 hello 組織使用者的存取權限。</span><span class="sxs-lookup"><span data-stu-id="0ac29-328">You can remove hello access permission for a user who is not managing hello Automation Account, or who no longer works for hello organization.</span></span> <span data-ttu-id="0ac29-329">下列是 hello 步驟 tooremove 使用者：</span><span class="sxs-lookup"><span data-stu-id="0ac29-329">Following are hello steps tooremove a user:</span></span> 

1. <span data-ttu-id="0ac29-330">從 hello**使用者**刀鋒視窗中，您想 tooremove 選取 hello 角色指派。</span><span class="sxs-lookup"><span data-stu-id="0ac29-330">From hello **Users** blade, select hello role assignment that you wish tooremove.</span></span>
2. <span data-ttu-id="0ac29-331">按一下 hello**移除**hello 分派詳細資料 刀鋒視窗中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0ac29-331">Click hello **Remove** button in hello assignment details blade.</span></span>
3. <span data-ttu-id="0ac29-332">按一下**是**tooconfirm 移除。</span><span class="sxs-lookup"><span data-stu-id="0ac29-332">Click **Yes** tooconfirm removal.</span></span> 
   
   ![移除使用者](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a><span data-ttu-id="0ac29-334">角色指派的使用者</span><span class="sxs-lookup"><span data-stu-id="0ac29-334">Role Assigned User</span></span>
<span data-ttu-id="0ac29-335">Tooa 角色指派的使用者登入時 tootheir 自動化帳戶，就可以看到 hello 清單中所列的擁有者 hello 帳戶**預設目錄**。</span><span class="sxs-lookup"><span data-stu-id="0ac29-335">When a user assigned tooa role logs in tootheir Automation account, they can now see hello owner’s account listed in hello list of **Default Directories**.</span></span> <span data-ttu-id="0ac29-336">在自動化帳戶加入至訂單 tooview hello，它們必須切換 hello 預設目錄 toohello 擁有者的預設目錄。</span><span class="sxs-lookup"><span data-stu-id="0ac29-336">In order tooview hello Automation account that they have been added to, they must switch hello default directory toohello owner’s default directory.</span></span>  

![預設目錄](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a><span data-ttu-id="0ac29-338">自動化操作員角色的使用者經驗</span><span class="sxs-lookup"><span data-stu-id="0ac29-338">User experience for Automation operator role</span></span>
<span data-ttu-id="0ac29-339">當指派 toohello 自動化操作員角色檢視 hello 自動化帳戶指派給使用者，是時，他們可以只檢視 runbook 的 hello 清單時，runbook 作業和排程 hello 自動化帳戶中建立，但無法檢視其定義。</span><span class="sxs-lookup"><span data-stu-id="0ac29-339">When a user, who is assigned toohello Automation Operator role views hello Automation account they are assigned to, they can only view hello list of runbooks, runbook jobs and schedules created in hello Automation account but can’t view their definition.</span></span> <span data-ttu-id="0ac29-340">他們可以啟動、 停止、 暫停、 繼續或排程 hello runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-340">They can start, stop, suspend, resume or schedule hello runbook job.</span></span> <span data-ttu-id="0ac29-341">hello 使用者不會有存取 tooother 自動化資源，例如混合式背景工作群組或 DSC 節點的組態。</span><span class="sxs-lookup"><span data-stu-id="0ac29-341">hello user will not have access tooother Automation resources such as configurations, hybrid worker groups or DSC nodes.</span></span>  

![沒有存取 tooresourcres](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

<span data-ttu-id="0ac29-343">當 hello 使用者按一下 hello runbook 時，hello tooview hello 來源，或編輯 hello runbook 的命令不提供為 hello 自動化操作員角色不允許存取 toothem。</span><span class="sxs-lookup"><span data-stu-id="0ac29-343">When hello user clicks on hello runbook, hello commands tooview hello source or edit hello runbook are not provided as hello Automation operator role doesn’t allow access toothem.</span></span>  

![沒有存取 tooedit runbook](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

<span data-ttu-id="0ac29-345">hello 使用者會有存取 tooview 和 toocreate 排程，但不是會存取 tooany 其他資產類型。</span><span class="sxs-lookup"><span data-stu-id="0ac29-345">hello user will have access tooview and toocreate schedules but will not have access tooany other asset type.</span></span>  

![沒有存取 tooassets](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

<span data-ttu-id="0ac29-347">此使用者也不具與 runbook 相關聯的存取 tooview hello webhook</span><span class="sxs-lookup"><span data-stu-id="0ac29-347">This user also doesn’t have access tooview hello webhooks associated with a runbook</span></span>

![沒有存取 toowebhooks](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a><span data-ttu-id="0ac29-349">使用 Azure PowerShell 為您的自動化帳戶設定 RBAC</span><span class="sxs-lookup"><span data-stu-id="0ac29-349">Configure RBAC for your Automation Account using Azure PowerShell</span></span>
<span data-ttu-id="0ac29-350">以角色為基礎的存取也可以設定的 tooan 自動化帳戶使用 hello 下列[Azure PowerShell cmdlet](../active-directory/role-based-access-control-manage-access-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="0ac29-350">Role-based access can also be configured tooan Automation Account using hello following [Azure PowerShell cmdlets](../active-directory/role-based-access-control-manage-access-powershell.md).</span></span>

<span data-ttu-id="0ac29-351">• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) 會列出 Azure Active Directory 中可用的所有 RBAC 角色。</span><span class="sxs-lookup"><span data-stu-id="0ac29-351">• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) lists all RBAC roles that are available in Azure Active Directory.</span></span> <span data-ttu-id="0ac29-352">您可以使用這個命令以及 hello**名稱**屬性 toolist 所有 hello 可由特定角色執行的動作。</span><span class="sxs-lookup"><span data-stu-id="0ac29-352">You can use this command along with hello **Name** property toolist all hello actions that can be performed by a specific role.</span></span>  
    <span data-ttu-id="0ac29-353">**範例：**</span><span class="sxs-lookup"><span data-stu-id="0ac29-353">**Example:**</span></span>  
    <span data-ttu-id="0ac29-354">![取得角色定義](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)</span><span class="sxs-lookup"><span data-stu-id="0ac29-354">![Get role definition](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)</span></span>  

<span data-ttu-id="0ac29-355">• [Get AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx)清單在 hello Azure AD RBAC 角色指派指定的範圍。</span><span class="sxs-lookup"><span data-stu-id="0ac29-355">• [Get-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) lists Azure AD RBAC role assignments at hello specified scope.</span></span> <span data-ttu-id="0ac29-356">如果沒有任何參數，此命令會傳回 hello 訂用帳戶底下所做的所有 hello 角色指派。</span><span class="sxs-lookup"><span data-stu-id="0ac29-356">Without any parameters, this command returns all hello role assignments made under hello subscription.</span></span> <span data-ttu-id="0ac29-357">使用 hello **ExpandPrincipalGroups**參數 toolist 存取指派 hello 可讓您指定使用者，以及 hello 群組 hello 使用者是的成員。</span><span class="sxs-lookup"><span data-stu-id="0ac29-357">Use hello **ExpandPrincipalGroups** parameter toolist access assignments for hello specified user as well as hello groups hello user is a member of.</span></span>  
    <span data-ttu-id="0ac29-358">**範例：**使用 hello 下列命令 toolist，hello 的所有使用者和其自動化帳戶內的角色。</span><span class="sxs-lookup"><span data-stu-id="0ac29-358">**Example:** Use hello following command toolist all hello users and their roles within an automation account.</span></span>

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![取得角色指派](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

<span data-ttu-id="0ac29-360">•[新增 AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign 存取 toousers、 群組和應用程式 tooa 特定範圍內。</span><span class="sxs-lookup"><span data-stu-id="0ac29-360">• [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign access toousers, groups and applications tooa particular scope.</span></span>  
    <span data-ttu-id="0ac29-361">**範例：**使用 hello 下列命令 tooassign hello"自動化操作員 」 角色 hello 自動化帳戶的範圍中的使用者。</span><span class="sxs-lookup"><span data-stu-id="0ac29-361">**Example:** Use hello following command tooassign hello “Automation Operator” role for a user in hello Automation Account scope.</span></span>

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![新角色指派](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

<span data-ttu-id="0ac29-363">• 使用[移除 AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) tooremove 存取指定的使用者、 群組或從特定範圍的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ac29-363">• Use [Remove-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) tooremove access of a specified user, group or application from a particular scope.</span></span>  
    <span data-ttu-id="0ac29-364">**範例：**使用 hello 下列命令 tooremove hello 使用者從 hello 自動化帳戶的範圍中的 hello"自動化操作員 」 角色。</span><span class="sxs-lookup"><span data-stu-id="0ac29-364">**Example:** Use hello following command tooremove hello user from hello “Automation Operator” role in hello Automation Account scope.</span></span>

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

<span data-ttu-id="0ac29-365">在上述範例 hello，取代**登入識別碼**，**訂用帳戶 Id**，**資源群組名稱**和**自動化帳戶名稱**與您帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0ac29-365">In hello above examples, replace **sign in Id**, **subscription Id**, **resource group name** and **Automation account name** with your account details.</span></span> <span data-ttu-id="0ac29-366">選擇**是**時提示 tooconfirm 才能繼續 tooremove 使用者角色指派。</span><span class="sxs-lookup"><span data-stu-id="0ac29-366">Choose **yes** when prompted tooconfirm before continuing tooremove user role assignment.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="0ac29-367">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ac29-367">Next Steps</span></span>
* <span data-ttu-id="0ac29-368">如需不同的方式 tooconfigure RBAC Azure 自動化的資訊，請參閱太[管理使用 Azure PowerShell RBAC](../active-directory/role-based-access-control-manage-access-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="0ac29-368">For information on different ways tooconfigure RBAC for Azure Automation, refer too[manage RBAC with Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).</span></span>
* <span data-ttu-id="0ac29-369">如需不同的方式 toostart runbook 的詳細資訊，請參閱[啟動 runbook](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0ac29-369">For details on different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md)</span></span>
* <span data-ttu-id="0ac29-370">如需不同的 runbook 類型資訊，請參閱太[Azure 自動化 runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="0ac29-370">For information about different runbook types, refer too[Azure Automation runbook types](automation-runbook-types.md)</span></span>

