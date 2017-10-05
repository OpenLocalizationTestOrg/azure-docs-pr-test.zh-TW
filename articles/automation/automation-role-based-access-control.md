---
title: "Azure 自動化中的角色型存取控制 | Microsoft Docs"
description: "角色型存取控制 (RBAC) 可以啟用對 Azure 資源的存取權管理。 本文說明如何在 Azure 自動化中設定 RBAC。"
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
ms.openlocfilehash: 17c7e410a9c5b69ab450eb3affd192f1e3cb6e76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="role-based-access-control-in-azure-automation"></a><span data-ttu-id="4e63a-105">Azure 自動化中的角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="4e63a-105">Role-based access control in Azure Automation</span></span>
## <a name="role-based-access-control"></a><span data-ttu-id="4e63a-106">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="4e63a-106">Role-based access control</span></span>
<span data-ttu-id="4e63a-107">角色型存取控制 (RBAC) 可以啟用對 Azure 資源的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="4e63a-107">Role-based access control (RBAC) enables access management for Azure resources.</span></span> <span data-ttu-id="4e63a-108">您可以使用 [RBAC](../active-directory/role-based-access-control-configure.md)來區隔小組內的職責，僅授與使用者、群組和應用程式執行作業所需的存取量。</span><span class="sxs-lookup"><span data-stu-id="4e63a-108">Using [RBAC](../active-directory/role-based-access-control-configure.md), you can segregate duties within your team and grant only the amount of access to users, groups and applications that they need to perform their jobs.</span></span> <span data-ttu-id="4e63a-109">使用 Azure 入口網站、Azure 命令列工具或 Azure 管理 API 的使用者，可以獲授與角色型存取權。</span><span class="sxs-lookup"><span data-stu-id="4e63a-109">Role-based access can be granted to users using the Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

## <a name="rbac-in-automation-accounts"></a><span data-ttu-id="4e63a-110">自動化帳戶中的 RBAC</span><span class="sxs-lookup"><span data-stu-id="4e63a-110">RBAC in Automation Accounts</span></span>
<span data-ttu-id="4e63a-111">在 Azure 自動化中，於自動化帳戶範圍將適當的 RBAC 角色指派給使用者、群組和應用程式，即可授與存取權。</span><span class="sxs-lookup"><span data-stu-id="4e63a-111">In Azure Automation, access is granted by assigning the appropriate RBAC role to users, groups, and applications at the Automation account scope.</span></span> <span data-ttu-id="4e63a-112">以下是自動化帳戶支援的內建角色：</span><span class="sxs-lookup"><span data-stu-id="4e63a-112">Following are the built-in roles supported by an Automation account:</span></span>  

| <span data-ttu-id="4e63a-113">**角色**</span><span class="sxs-lookup"><span data-stu-id="4e63a-113">**Role**</span></span> | <span data-ttu-id="4e63a-114">**說明**</span><span class="sxs-lookup"><span data-stu-id="4e63a-114">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e63a-115">擁有者</span><span class="sxs-lookup"><span data-stu-id="4e63a-115">Owner</span></span> |<span data-ttu-id="4e63a-116">擁有者角色允許存取自動化帳戶中的所有資源和動作，包括存取提供給其他使用者、群組和應用程式，以管理自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e63a-116">The Owner role allows access to all resources and actions within an Automation account including providing access to other users, groups and applications to manage the Automation account.</span></span> |
| <span data-ttu-id="4e63a-117">參與者</span><span class="sxs-lookup"><span data-stu-id="4e63a-117">Contributor</span></span> |<span data-ttu-id="4e63a-118">參與者角色可讓您管理各個項目，修改其他使用者的自動化帳戶存取權限除外。</span><span class="sxs-lookup"><span data-stu-id="4e63a-118">The Contributor role allows you to manage everything except modifying other user’s access permissions to an Automation account.</span></span> |
| <span data-ttu-id="4e63a-119">讀取者</span><span class="sxs-lookup"><span data-stu-id="4e63a-119">Reader</span></span> |<span data-ttu-id="4e63a-120">讀取者角色可讓您檢視自動化帳戶中的所有資源，但無法進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="4e63a-120">The Reader role allows you to view all the resources in an Automation account but cannot make any changes.</span></span> |
| <span data-ttu-id="4e63a-121">自動化運算子</span><span class="sxs-lookup"><span data-stu-id="4e63a-121">Automation Operator</span></span> |<span data-ttu-id="4e63a-122">自動化操作員角色可讓您執行作業的工作，例如啟動、停止、暫停、繼續和排程作業。</span><span class="sxs-lookup"><span data-stu-id="4e63a-122">The Automation Operator role allows you to perform operational tasks such as start, stop, suspend, resume and schedule jobs.</span></span> <span data-ttu-id="4e63a-123">如果您想要保護認證資產和 Runbook 等自動化帳戶資源不被檢視或修改，但仍然允許組織的成員來執行這些 Runbook，這個角色會有所幫助。</span><span class="sxs-lookup"><span data-stu-id="4e63a-123">This role is helpful if you want to protect your Automation Account resources like credentials assets and runbooks from being viewed or modified but still allow members of your organization to execute these runbooks.</span></span> |
| <span data-ttu-id="4e63a-124">使用者存取系統管理員</span><span class="sxs-lookup"><span data-stu-id="4e63a-124">User Access Administrator</span></span> |<span data-ttu-id="4e63a-125">使用者存取系統管理員角色可讓您管理 Azure 自動化帳戶的使用者存取。</span><span class="sxs-lookup"><span data-stu-id="4e63a-125">The User Access Administrator role allows you to manage user access to Azure Automation accounts.</span></span> |

> [!NOTE]
> <span data-ttu-id="4e63a-126">您無法授與特定 Runbook 的存取權限，只能授與自動化帳戶內資源和動作的存取權限。</span><span class="sxs-lookup"><span data-stu-id="4e63a-126">You cannot grant access rights to a specific runbook or runbooks, only to the resources and actions within the Automation account.</span></span>  
> 
> 

<span data-ttu-id="4e63a-127">在本文中，我們將逐步引導您如何在 Azure 自動化中設定 RBAC。</span><span class="sxs-lookup"><span data-stu-id="4e63a-127">In this article we will walk you through how to set up RBAC in Azure Automation.</span></span> <span data-ttu-id="4e63a-128">但首先，讓我們深入探討授與給參與者、讀取者、自動化操作員和使用者存取系統管理員的個別權限，以便在將自動化帳戶的權限授與給任何人前充分瞭解相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4e63a-128">But first, let's take a closer look at the individual permissions granted to the Contributor, Reader, Automation Operator and User Access Administrator so that we gain a good understanding before granting anyone rights to the Automation account.</span></span>  <span data-ttu-id="4e63a-129">否則，可能會造成非預期或不想要的結果。</span><span class="sxs-lookup"><span data-stu-id="4e63a-129">Otherwise it could result in unintended or undesirable consequences.</span></span>     

## <a name="contributor-role-permissions"></a><span data-ttu-id="4e63a-130">參與者角色權限</span><span class="sxs-lookup"><span data-stu-id="4e63a-130">Contributor role permissions</span></span>
<span data-ttu-id="4e63a-131">下表顯示參與者角色可以在自動化中執行的特定動作。</span><span class="sxs-lookup"><span data-stu-id="4e63a-131">The following table presents the specific actions that can be performed by the Contributor role in Automation.</span></span>

| <span data-ttu-id="4e63a-132">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="4e63a-132">**Resource Type**</span></span> | <span data-ttu-id="4e63a-133">**讀取**</span><span class="sxs-lookup"><span data-stu-id="4e63a-133">**Read**</span></span> | <span data-ttu-id="4e63a-134">**寫入**</span><span class="sxs-lookup"><span data-stu-id="4e63a-134">**Write**</span></span> | <span data-ttu-id="4e63a-135">**刪除**</span><span class="sxs-lookup"><span data-stu-id="4e63a-135">**Delete**</span></span> | <span data-ttu-id="4e63a-136">**其他動作**</span><span class="sxs-lookup"><span data-stu-id="4e63a-136">**Other Actions**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="4e63a-137">Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="4e63a-137">Azure Automation Account</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-141">自動化憑證資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-141">Automation Certificate Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-145">自動化連線資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-145">Automation Connection Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-149">自動化連線類型資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-149">Automation Connection Type Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-153">自動化認證資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-153">Automation Credential Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-157">自動化排程資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-157">Automation Schedule Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-161">自動化變數資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-161">Automation Variable Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-165">自動化期望狀態組態</span><span class="sxs-lookup"><span data-stu-id="4e63a-165">Automation Desired State Configuration</span></span> | | | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="4e63a-167">Hybrid Runbook Worker 類型</span><span class="sxs-lookup"><span data-stu-id="4e63a-167">Hybrid Runbook Worker Resource Type</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-170">Azure 自動化作業</span><span class="sxs-lookup"><span data-stu-id="4e63a-170">Azure Automation Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="4e63a-174">自動化作業串流</span><span class="sxs-lookup"><span data-stu-id="4e63a-174">Automation Job Stream</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-176">自動化作業排程</span><span class="sxs-lookup"><span data-stu-id="4e63a-176">Automation Job Schedule</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-180">自動化模組</span><span class="sxs-lookup"><span data-stu-id="4e63a-180">Automation Module</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |
| <span data-ttu-id="4e63a-184">Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="4e63a-184">Azure Automation Runbook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="4e63a-189">自動化 Runbook 草稿</span><span class="sxs-lookup"><span data-stu-id="4e63a-189">Automation Runbook Draft</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="4e63a-192">自動化 Runbook 草稿測試作業</span><span class="sxs-lookup"><span data-stu-id="4e63a-192">Automation Runbook Draft Test Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="4e63a-196">自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="4e63a-196">Automation Webhook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a><span data-ttu-id="4e63a-201">讀取者角色權限</span><span class="sxs-lookup"><span data-stu-id="4e63a-201">Reader role permissions</span></span>
<span data-ttu-id="4e63a-202">下表顯示讀取者角色可以在自動化中執行的特定動作。</span><span class="sxs-lookup"><span data-stu-id="4e63a-202">The following table presents the specific actions that can be performed by the Reader role in Automation.</span></span>

| <span data-ttu-id="4e63a-203">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="4e63a-203">**Resource Type**</span></span> | <span data-ttu-id="4e63a-204">**讀取**</span><span class="sxs-lookup"><span data-stu-id="4e63a-204">**Read**</span></span> | <span data-ttu-id="4e63a-205">**寫入**</span><span class="sxs-lookup"><span data-stu-id="4e63a-205">**Write**</span></span> | <span data-ttu-id="4e63a-206">**刪除**</span><span class="sxs-lookup"><span data-stu-id="4e63a-206">**Delete**</span></span> | <span data-ttu-id="4e63a-207">**其他動作**</span><span class="sxs-lookup"><span data-stu-id="4e63a-207">**Other Actions**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="4e63a-208">傳統訂用帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="4e63a-208">Classic subscription administrator</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-210">管理鎖定</span><span class="sxs-lookup"><span data-stu-id="4e63a-210">Management lock</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-212">權限</span><span class="sxs-lookup"><span data-stu-id="4e63a-212">Permission</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-214">提供者作業</span><span class="sxs-lookup"><span data-stu-id="4e63a-214">Provider operations</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-216">角色指派</span><span class="sxs-lookup"><span data-stu-id="4e63a-216">Role assignment</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-218">角色定義</span><span class="sxs-lookup"><span data-stu-id="4e63a-218">Role definition</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a><span data-ttu-id="4e63a-220">自動化操作員角色權限</span><span class="sxs-lookup"><span data-stu-id="4e63a-220">Automation Operator role permissions</span></span>
<span data-ttu-id="4e63a-221">下表顯示自動化操作員角色可以在自動化中執行的特定動作。</span><span class="sxs-lookup"><span data-stu-id="4e63a-221">The following table presents the specific actions that can be performed by the Automation Operator role in Automation.</span></span>

| <span data-ttu-id="4e63a-222">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="4e63a-222">**Resource Type**</span></span> | <span data-ttu-id="4e63a-223">**讀取**</span><span class="sxs-lookup"><span data-stu-id="4e63a-223">**Read**</span></span> | <span data-ttu-id="4e63a-224">**寫入**</span><span class="sxs-lookup"><span data-stu-id="4e63a-224">**Write**</span></span> | <span data-ttu-id="4e63a-225">**刪除**</span><span class="sxs-lookup"><span data-stu-id="4e63a-225">**Delete**</span></span> | <span data-ttu-id="4e63a-226">**其他動作**</span><span class="sxs-lookup"><span data-stu-id="4e63a-226">**Other Actions**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="4e63a-227">Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="4e63a-227">Azure Automation Account</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-229">自動化憑證資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-229">Automation Certificate Asset</span></span> | | | | |
| <span data-ttu-id="4e63a-230">自動化連線資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-230">Automation Connection Asset</span></span> | | | | |
| <span data-ttu-id="4e63a-231">自動化連線類型資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-231">Automation Connection Type Asset</span></span> | | | | |
| <span data-ttu-id="4e63a-232">自動化認證資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-232">Automation Credential Asset</span></span> | | | | |
| <span data-ttu-id="4e63a-233">自動化排程資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-233">Automation Schedule Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |
| <span data-ttu-id="4e63a-236">自動化變數資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-236">Automation Variable Asset</span></span> | | | | |
| <span data-ttu-id="4e63a-237">自動化期望狀態組態</span><span class="sxs-lookup"><span data-stu-id="4e63a-237">Automation Desired State Configuration</span></span> | | | | |
| <span data-ttu-id="4e63a-238">Hybrid Runbook Worker 類型</span><span class="sxs-lookup"><span data-stu-id="4e63a-238">Hybrid Runbook Worker Resource Type</span></span> | | | | |
| <span data-ttu-id="4e63a-239">Azure 自動化作業</span><span class="sxs-lookup"><span data-stu-id="4e63a-239">Azure Automation Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |
| <span data-ttu-id="4e63a-243">自動化作業串流</span><span class="sxs-lookup"><span data-stu-id="4e63a-243">Automation Job Stream</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-245">自動化作業排程</span><span class="sxs-lookup"><span data-stu-id="4e63a-245">Automation Job Schedule</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | |
| <span data-ttu-id="4e63a-248">自動化模組</span><span class="sxs-lookup"><span data-stu-id="4e63a-248">Automation Module</span></span> | | | | |
| <span data-ttu-id="4e63a-249">Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="4e63a-249">Azure Automation Runbook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-251">自動化 Runbook 草稿</span><span class="sxs-lookup"><span data-stu-id="4e63a-251">Automation Runbook Draft</span></span> | | | | |
| <span data-ttu-id="4e63a-252">自動化 Runbook 草稿測試作業</span><span class="sxs-lookup"><span data-stu-id="4e63a-252">Automation Runbook Draft Test Job</span></span> | | | | |
| <span data-ttu-id="4e63a-253">自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="4e63a-253">Automation Webhook</span></span> | | | | |

<span data-ttu-id="4e63a-254">如需進一步詳細資訊， [自動化操作員動作](../active-directory/role-based-access-built-in-roles.md#automation-operator) 會列出自動化帳戶和其資源的自動化操作員角色所支援的動作。</span><span class="sxs-lookup"><span data-stu-id="4e63a-254">For further details, the [Automation operator actions](../active-directory/role-based-access-built-in-roles.md#automation-operator) lists the actions supported by the Automation operator role on the Automation account and its resources.</span></span>

## <a name="user-access-administrator-role-permissions"></a><span data-ttu-id="4e63a-255">使用者存取系統管理員角色權限</span><span class="sxs-lookup"><span data-stu-id="4e63a-255">User Access Administrator role permissions</span></span>
<span data-ttu-id="4e63a-256">下表顯示使用者存取系統管理員角色可以在自動化中執行的特定動作。</span><span class="sxs-lookup"><span data-stu-id="4e63a-256">The following table presents the specific actions that can be performed by the User Access Administrator role in Automation.</span></span>

| <span data-ttu-id="4e63a-257">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="4e63a-257">**Resource Type**</span></span> | <span data-ttu-id="4e63a-258">**讀取**</span><span class="sxs-lookup"><span data-stu-id="4e63a-258">**Read**</span></span> | <span data-ttu-id="4e63a-259">**寫入**</span><span class="sxs-lookup"><span data-stu-id="4e63a-259">**Write**</span></span> | <span data-ttu-id="4e63a-260">**刪除**</span><span class="sxs-lookup"><span data-stu-id="4e63a-260">**Delete**</span></span> | <span data-ttu-id="4e63a-261">**其他動作**</span><span class="sxs-lookup"><span data-stu-id="4e63a-261">**Other Actions**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="4e63a-262">Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="4e63a-262">Azure Automation Account</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-264">自動化憑證資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-264">Automation Certificate Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-266">自動化連線資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-266">Automation Connection Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-268">自動化連線類型資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-268">Automation Connection Type Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-270">自動化認證資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-270">Automation Credential Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-272">自動化排程資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-272">Automation Schedule Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-274">自動化變數資產</span><span class="sxs-lookup"><span data-stu-id="4e63a-274">Automation Variable Asset</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-276">自動化期望狀態組態</span><span class="sxs-lookup"><span data-stu-id="4e63a-276">Automation Desired State Configuration</span></span> | | | | |
| <span data-ttu-id="4e63a-277">Hybrid Runbook Worker 類型</span><span class="sxs-lookup"><span data-stu-id="4e63a-277">Hybrid Runbook Worker Resource Type</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-279">Azure 自動化作業</span><span class="sxs-lookup"><span data-stu-id="4e63a-279">Azure Automation Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-281">自動化作業串流</span><span class="sxs-lookup"><span data-stu-id="4e63a-281">Automation Job Stream</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-283">自動化作業排程</span><span class="sxs-lookup"><span data-stu-id="4e63a-283">Automation Job Schedule</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-285">自動化模組</span><span class="sxs-lookup"><span data-stu-id="4e63a-285">Automation Module</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-287">Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="4e63a-287">Azure Automation Runbook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-289">自動化 Runbook 草稿</span><span class="sxs-lookup"><span data-stu-id="4e63a-289">Automation Runbook Draft</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-291">自動化 Runbook 草稿測試作業</span><span class="sxs-lookup"><span data-stu-id="4e63a-291">Automation Runbook Draft Test Job</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |
| <span data-ttu-id="4e63a-293">自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="4e63a-293">Automation Webhook</span></span> |![綠色狀態](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a><span data-ttu-id="4e63a-295">使用 Azure 入口網站為您的自動化帳戶設定 RBAC</span><span class="sxs-lookup"><span data-stu-id="4e63a-295">Configure RBAC for your Automation Account using Azure Portal</span></span>
1. <span data-ttu-id="4e63a-296">登入 [Azure 入口網站](https://portal.azure.com/) ，並從 [自動化帳戶] 刀鋒視窗開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e63a-296">Log in to the [Azure Portal](https://portal.azure.com/) and open your Automation account from the Automation Accounts blade.</span></span>  
2. <span data-ttu-id="4e63a-297">按一下右上角的 [存取]  控制項。</span><span class="sxs-lookup"><span data-stu-id="4e63a-297">Click on the **Access** control at the top right corner.</span></span> <span data-ttu-id="4e63a-298">這會開啟 [使用者]  刀鋒視窗，您可以在其中加入新使用者、群組及應用程式來管理您的自動化帳戶，並檢視可以為自動化帳戶設定的現有角色。</span><span class="sxs-lookup"><span data-stu-id="4e63a-298">This opens the **Users** blade where you can add new users, groups and applications to manage your Automation account and view existing roles that can be configured for the Automation Account.</span></span>  
   
   ![[存取] 按鈕](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> <span data-ttu-id="4e63a-300">**訂用帳戶管理員** 已經存在做為預設的使用者。</span><span class="sxs-lookup"><span data-stu-id="4e63a-300">**Subscription admins** already exists as the default user.</span></span> <span data-ttu-id="4e63a-301">訂用帳戶管理員 Active Directory 群組包含服務系統管理員和 Azure 訂用帳戶的共同管理員。</span><span class="sxs-lookup"><span data-stu-id="4e63a-301">The subscription admins active directory group includes the service administrator(s) and co-administrator(s) for your Azure subscription.</span></span> <span data-ttu-id="4e63a-302">服務系統管理員為您的 Azure 訂用帳戶和其資源的擁有者，而且會具有對自動化帳戶繼承的擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="4e63a-302">The Service admin is the owner of your Azure subscription and its resources, and will have the owner role inherited for the automation accounts too.</span></span> <span data-ttu-id="4e63a-303">這表示存取權是由訂用帳戶的**服務系統管理員和共同管理員****繼承**，並且針對所有其他的使用者**指派**。</span><span class="sxs-lookup"><span data-stu-id="4e63a-303">This means that the access is **Inherited** for **service administrators and co-admins** of a subscription and it’s **Assigned** for all the other users.</span></span> <span data-ttu-id="4e63a-304">按一下 [訂用帳戶管理員]  來檢視有關其權限的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4e63a-304">Click **Subscription admins** to view more details about their permissions.</span></span>  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a><span data-ttu-id="4e63a-305">加入新使用者並指派角色</span><span class="sxs-lookup"><span data-stu-id="4e63a-305">Add a new user and assign a role</span></span>
1. <span data-ttu-id="4e63a-306">從 [使用者] 刀鋒視窗中，按一下 [新增] 以開啟 [新增存取] 刀鋒視窗，您可以在其中新增使用者、群組或應用程式，並將角色指派給他們。</span><span class="sxs-lookup"><span data-stu-id="4e63a-306">From the Users blade, click **Add** to open the **Add access blade** where you can add a user, group, or application, and assign a role to them.</span></span>  
   
   ![新增使用者](media/automation-role-based-access-control/automation-02-add-user.png)  
2. <span data-ttu-id="4e63a-308">從可用角色的清單中選取角色。</span><span class="sxs-lookup"><span data-stu-id="4e63a-308">Select a role from the list of available roles.</span></span> <span data-ttu-id="4e63a-309">我們將選擇 **讀取者** 角色，但是您可以選擇自動化帳戶支援的任何可用的內建角色，或已定義的任何自訂角色。</span><span class="sxs-lookup"><span data-stu-id="4e63a-309">We will choose the **Reader** role, but you can choose any of the available built-in roles that an Automation Account supports or any custom role you may have defined.</span></span>  
   
   ![選取角色](media/automation-role-based-access-control/automation-03-select-role.png)  
3. <span data-ttu-id="4e63a-311">按一下 [新增使用者] 以開啟 [新增使用者] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4e63a-311">Click on **Add users** to open the **Add users** blade.</span></span> <span data-ttu-id="4e63a-312">如果您已新增任何使用者、群組或應用程式以管理您的訂用帳戶，則會列出這些使用者，您可以選取他們以新增存取權。</span><span class="sxs-lookup"><span data-stu-id="4e63a-312">If you have added any users, groups, or applications to manage your subscription then those users are listed and you can select them to add access.</span></span> <span data-ttu-id="4e63a-313">如果沒有列出任何使用者，或未列出您有興趣新增的使用者，請按一下 [邀請] 開啟 [邀請來賓] 刀鋒視窗；您可以在此邀請具有有效 Microsoft 帳戶電子郵件地址 (例如 Outlook.com、OneDrive 或 Xbox Live ID) 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4e63a-313">If there aren’t any users listed, or if the user you are interested in adding is not listed then click **invite** to open the **Invite a guest** blade, where you can invite a user with a valid Microsoft account email address such as Outlook.com, OneDrive, or Xbox Live Ids.</span></span> <span data-ttu-id="4e63a-314">輸入了使用者的電子郵件地址之後，按一下 [選取] 以新增使用者，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4e63a-314">Once you have entered the email address of the user, click **Select** to add the user, and then click **OK**.</span></span> 
   
   ![新增使用者](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   <span data-ttu-id="4e63a-316">現在您應該會看到使用者新增至 [使用者] 刀鋒視窗，並且獲指派**讀取者**角色。</span><span class="sxs-lookup"><span data-stu-id="4e63a-316">Now you should see the user added to the **Users** blade with the **Reader** role assigned.</span></span>  
   
   ![列出使用者](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   <span data-ttu-id="4e63a-318">您也可以從 [角色]  刀鋒視窗指派角色給使用者。</span><span class="sxs-lookup"><span data-stu-id="4e63a-318">You can also assign a role to the user from the **Roles** blade.</span></span> 
4. <span data-ttu-id="4e63a-319">從 [使用者] 刀鋒視窗按一下 [角色] 以開啟 [角色] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4e63a-319">Click **Roles** from the Users blade to open the **Roles blade**.</span></span> <span data-ttu-id="4e63a-320">從這個刀鋒視窗中，您可以檢視角色的名稱、指派給該角色的使用者和群組數目。</span><span class="sxs-lookup"><span data-stu-id="4e63a-320">From this blade, you can view the name of the role, the number of users and groups assigned to that role.</span></span>
   
    ![從 [使用者] 刀鋒視窗指派角色](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > <span data-ttu-id="4e63a-322">只能在自動化帳戶層級，而非低於自動化帳戶的任何資源中設定以角色為基礎的存取控制。</span><span class="sxs-lookup"><span data-stu-id="4e63a-322">Role-based access control can only be set at the Automation Account level and not at any resource below the Automation Account.</span></span>
   > 
   > 
   
    <span data-ttu-id="4e63a-323">您可以將多個角色指派給使用者、群組或應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e63a-323">You can assign more than one role to a user, group, or application.</span></span> <span data-ttu-id="4e63a-324">例如，如果我們新增**自動化操作員**角色連同**讀取者角色**給使用者，那麼他們可以檢視所有的自動化資源，以及執行 Runbook 作業。</span><span class="sxs-lookup"><span data-stu-id="4e63a-324">For example, if we add the **Automation Operator** role along with the **Reader role** to the user, then they can view all the Automation resources, as well as execute the runbook jobs.</span></span> <span data-ttu-id="4e63a-325">您可以展開下拉式清單以檢視指派給使用者的角色清單。</span><span class="sxs-lookup"><span data-stu-id="4e63a-325">You can expand the dropdown to view a list of roles assigned to the user.</span></span>  
   
    ![檢視多個角色](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a><span data-ttu-id="4e63a-327">移除使用者</span><span class="sxs-lookup"><span data-stu-id="4e63a-327">Remove a user</span></span>
<span data-ttu-id="4e63a-328">您可以移除未管理自動化帳戶的使用者，或不再為組織工作之使用者的存取權限。</span><span class="sxs-lookup"><span data-stu-id="4e63a-328">You can remove the access permission for a user who is not managing the Automation Account, or who no longer works for the organization.</span></span> <span data-ttu-id="4e63a-329">以下是移除使用者的步驟：</span><span class="sxs-lookup"><span data-stu-id="4e63a-329">Following are the steps to remove a user:</span></span> 

1. <span data-ttu-id="4e63a-330">從 [使用者]  刀鋒視窗中，選取您想要移除的角色指派。</span><span class="sxs-lookup"><span data-stu-id="4e63a-330">From the **Users** blade, select the role assignment that you wish to remove.</span></span>
2. <span data-ttu-id="4e63a-331">按一下指派詳細資料刀鋒視窗上的 [移除]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4e63a-331">Click the **Remove** button in the assignment details blade.</span></span>
3. <span data-ttu-id="4e63a-332">按一下 [是]  以確認移除。</span><span class="sxs-lookup"><span data-stu-id="4e63a-332">Click **Yes** to confirm removal.</span></span> 
   
   ![移除使用者](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a><span data-ttu-id="4e63a-334">角色指派的使用者</span><span class="sxs-lookup"><span data-stu-id="4e63a-334">Role Assigned User</span></span>
<span data-ttu-id="4e63a-335">當獲派角色的使用者登入他們的自動化帳戶時，可以看到擁有者的帳戶列於 **預設目錄**清單中。</span><span class="sxs-lookup"><span data-stu-id="4e63a-335">When a user assigned to a role logs in to their Automation account, they can now see the owner’s account listed in the list of **Default Directories**.</span></span> <span data-ttu-id="4e63a-336">若要檢視他們被加入的自動化帳戶，他們必須將預設目錄切換到擁有者的預設目錄。</span><span class="sxs-lookup"><span data-stu-id="4e63a-336">In order to view the Automation account that they have been added to, they must switch the default directory to the owner’s default directory.</span></span>  

![預設目錄](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a><span data-ttu-id="4e63a-338">自動化操作員角色的使用者經驗</span><span class="sxs-lookup"><span data-stu-id="4e63a-338">User experience for Automation operator role</span></span>
<span data-ttu-id="4e63a-339">當指派為自動化操作員角色的使用者檢視指派給他的自動化帳戶時，只能檢視在自動化帳戶中建立的 Runbook、Runbook 作業和排程的清單，但無法檢視其定義。</span><span class="sxs-lookup"><span data-stu-id="4e63a-339">When a user, who is assigned to the Automation Operator role views the Automation account they are assigned to, they can only view the list of runbooks, runbook jobs and schedules created in the Automation account but can’t view their definition.</span></span> <span data-ttu-id="4e63a-340">他們可以啟動、停止、暫停、繼續或排程 Runbook 作業。</span><span class="sxs-lookup"><span data-stu-id="4e63a-340">They can start, stop, suspend, resume or schedule the runbook job.</span></span> <span data-ttu-id="4e63a-341">使用者將無法存取其他自動化資源，例如組態、混合式背景工作群組或 DSC 節點。</span><span class="sxs-lookup"><span data-stu-id="4e63a-341">The user will not have access to other Automation resources such as configurations, hybrid worker groups or DSC nodes.</span></span>  

![沒有資源的存取權](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

<span data-ttu-id="4e63a-343">當使用者按一下 Runbook 時，不會提供檢視來源或編輯 Runbook 的命令，因為自動化操作員角色不允許存取它們。</span><span class="sxs-lookup"><span data-stu-id="4e63a-343">When the user clicks on the runbook, the commands to view the source or edit the runbook are not provided as the Automation operator role doesn’t allow access to them.</span></span>  

![沒有編輯 Runbook 的存取權](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

<span data-ttu-id="4e63a-345">使用者將可檢視及建立排程，但無法存取任何其他資產類型。</span><span class="sxs-lookup"><span data-stu-id="4e63a-345">The user will have access to view and to create schedules but will not have access to any other asset type.</span></span>  

![沒有資產的存取權](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

<span data-ttu-id="4e63a-347">這位使用者也沒有存取權可以檢視與 Runbook 相關聯的 Webhook</span><span class="sxs-lookup"><span data-stu-id="4e63a-347">This user also doesn’t have access to view the webhooks associated with a runbook</span></span>

![沒有 Webhook 的存取權](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a><span data-ttu-id="4e63a-349">使用 Azure PowerShell 為您的自動化帳戶設定 RBAC</span><span class="sxs-lookup"><span data-stu-id="4e63a-349">Configure RBAC for your Automation Account using Azure PowerShell</span></span>
<span data-ttu-id="4e63a-350">使用下列 [Azure PowerShell Cmdlet](../active-directory/role-based-access-control-manage-access-powershell.md)也可以將角色型存取設定到自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e63a-350">Role-based access can also be configured to an Automation Account using the following [Azure PowerShell cmdlets](../active-directory/role-based-access-control-manage-access-powershell.md).</span></span>

<span data-ttu-id="4e63a-351">• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) 會列出 Azure Active Directory 中可用的所有 RBAC 角色。</span><span class="sxs-lookup"><span data-stu-id="4e63a-351">• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) lists all RBAC roles that are available in Azure Active Directory.</span></span> <span data-ttu-id="4e63a-352">您可以使用這個命令搭配 [名稱] 屬性，列出特定角色可以執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="4e63a-352">You can use this command along with the **Name** property to list all the actions that can be performed by a specific role.</span></span>  
    <span data-ttu-id="4e63a-353">**範例：**</span><span class="sxs-lookup"><span data-stu-id="4e63a-353">**Example:**</span></span>  
    <span data-ttu-id="4e63a-354">![取得角色定義](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)</span><span class="sxs-lookup"><span data-stu-id="4e63a-354">![Get role definition](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)</span></span>  

<span data-ttu-id="4e63a-355">• [Get-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) 會列出在指定範圍的 Azure AD RBAC 角色指派。</span><span class="sxs-lookup"><span data-stu-id="4e63a-355">• [Get-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) lists Azure AD RBAC role assignments at the specified scope.</span></span> <span data-ttu-id="4e63a-356">如果沒有任何參數，此命令會傳回在訂用帳戶下所做的所有角色指派。</span><span class="sxs-lookup"><span data-stu-id="4e63a-356">Without any parameters, this command returns all the role assignments made under the subscription.</span></span> <span data-ttu-id="4e63a-357">使用 **ExpandPrincipalGroups** 參數，列出指定使用者以及使用者為其成員之群組的存取權指派。</span><span class="sxs-lookup"><span data-stu-id="4e63a-357">Use the **ExpandPrincipalGroups** parameter to list access assignments for the specified user as well as the groups the user is a member of.</span></span>  
    <span data-ttu-id="4e63a-358">**範例：**使用下列命令來列出自動化帳戶中的所有使用者以及其角色。</span><span class="sxs-lookup"><span data-stu-id="4e63a-358">**Example:** Use the following command to list all the users and their roles within an automation account.</span></span>

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![取得角色指派](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

<span data-ttu-id="4e63a-360">• [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) 可將使用者、群組和應用程式的存取權指派給特定範圍。</span><span class="sxs-lookup"><span data-stu-id="4e63a-360">• [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) to assign access to users, groups and applications to a particular scope.</span></span>  
    <span data-ttu-id="4e63a-361">**範例：**使用下列命令來為自動化帳戶範圍內的使用者指派「自動化操作員」角色。</span><span class="sxs-lookup"><span data-stu-id="4e63a-361">**Example:** Use the following command to assign the “Automation Operator” role for a user in the Automation Account scope.</span></span>

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish to grant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![新角色指派](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

<span data-ttu-id="4e63a-363">• 使用 [Remove-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) 來移除特定範圍內指定的使用者、群組或應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="4e63a-363">• Use [Remove-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) to remove access of a specified user, group or application from a particular scope.</span></span>  
    <span data-ttu-id="4e63a-364">**範例：**使用下列命令，從自動化帳戶範圍內的「自動化操作員」角色移除使用者。</span><span class="sxs-lookup"><span data-stu-id="4e63a-364">**Example:** Use the following command to remove the user from the “Automation Operator” role in the Automation Account scope.</span></span>

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish to remove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

<span data-ttu-id="4e63a-365">在上述範例中，請以您的帳戶詳細資料取代[登入識別碼]、[訂用帳戶識別碼]、[資源群組名稱] 和 [自動化帳戶名稱]。</span><span class="sxs-lookup"><span data-stu-id="4e63a-365">In the above examples, replace **sign in Id**, **subscription Id**, **resource group name** and **Automation account name** with your account details.</span></span> <span data-ttu-id="4e63a-366">當系統提示您確認時選擇 [是]  ，然後再繼續移除使用者角色指派。</span><span class="sxs-lookup"><span data-stu-id="4e63a-366">Choose **yes** when prompted to confirm before continuing to remove user role assignment.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="4e63a-367">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e63a-367">Next Steps</span></span>
* <span data-ttu-id="4e63a-368">如需針對 Azure 自動化設定 RBAC 的不同方式詳細資訊，請參閱 [使用 Azure PowerShell 管理 RBAC](../active-directory/role-based-access-control-manage-access-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="4e63a-368">For information on different ways to configure RBAC for Azure Automation, refer to [manage RBAC with Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).</span></span>
* <span data-ttu-id="4e63a-369">如需以不同方式啟動 Runbook 的詳細資訊，請參閱 [啟動 Runbook](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="4e63a-369">For details on different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md)</span></span>
* <span data-ttu-id="4e63a-370">如需不同 Runbook 類型的詳細資訊，請參閱 [Azure 自動化 Runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="4e63a-370">For information about different runbook types, refer to [Azure Automation runbook types](automation-runbook-types.md)</span></span>

