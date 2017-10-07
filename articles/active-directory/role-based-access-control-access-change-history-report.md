---
title: "報告 aaaAccess-Azure rbac 進行 |Microsoft 文件"
description: "產生報告，列出所有變更中存取 tooyour hello 的角色型存取控制與 Azure 訂用帳戶過去 90 天內。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="87594-103">建立角色型存取控制的存取報告</span><span class="sxs-lookup"><span data-stu-id="87594-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="87594-104">有人會授與或撤銷存取權，您的訂閱，在任何時間 hello 變更會記錄在 Azure 的事件。</span><span class="sxs-lookup"><span data-stu-id="87594-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="87594-105">您可以建立存取變更歷程記錄報表 toosee 所有變更的 hello 過去 90 天內。</span><span class="sxs-lookup"><span data-stu-id="87594-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="87594-106">使用 Azure PowerShell 建立報告</span><span class="sxs-lookup"><span data-stu-id="87594-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="87594-107">toocreate 存取變更歷程記錄報表，在 PowerShell 中，使用 hello [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog)命令。</span><span class="sxs-lookup"><span data-stu-id="87594-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="87594-108">當您呼叫此命令時，您可以指定您想要列出，包括 hello 下列 hello 分派的哪一個屬性：</span><span class="sxs-lookup"><span data-stu-id="87594-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="87594-109">屬性</span><span class="sxs-lookup"><span data-stu-id="87594-109">Property</span></span> | <span data-ttu-id="87594-110">說明</span><span class="sxs-lookup"><span data-stu-id="87594-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="87594-111">**Action**</span><span class="sxs-lookup"><span data-stu-id="87594-111">**Action**</span></span> |<span data-ttu-id="87594-112">已授與或已撤銷存取權</span><span class="sxs-lookup"><span data-stu-id="87594-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="87594-113">**Caller**</span><span class="sxs-lookup"><span data-stu-id="87594-113">**Caller**</span></span> |<span data-ttu-id="87594-114">負責 hello 存取 hello 擁有者變更</span><span class="sxs-lookup"><span data-stu-id="87594-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="87594-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="87594-115">**PrincipalId**</span></span> | <span data-ttu-id="87594-116">hello hello 使用者、 群組或指派 hello 角色的應用程式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="87594-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="87594-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="87594-117">**PrincipalName**</span></span> |<span data-ttu-id="87594-118">hello 名稱的 hello 使用者、 群組或應用程式</span><span class="sxs-lookup"><span data-stu-id="87594-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="87594-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="87594-119">**PrincipalType**</span></span> |<span data-ttu-id="87594-120">Hello 分派是否針對使用者、 群組或應用程式</span><span class="sxs-lookup"><span data-stu-id="87594-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="87594-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="87594-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="87594-122">hello hello 角色所授與或撤銷的 GUID</span><span class="sxs-lookup"><span data-stu-id="87594-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="87594-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="87594-123">**RoleName**</span></span> |<span data-ttu-id="87594-124">已授與或撤銷 hello 角色</span><span class="sxs-lookup"><span data-stu-id="87594-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="87594-125">**範圍**</span><span class="sxs-lookup"><span data-stu-id="87594-125">**Scope**</span></span> | <span data-ttu-id="87594-126">hello hello 訂用帳戶、 資源群組或 hello 分派的資源的唯一識別項太適用於</span><span class="sxs-lookup"><span data-stu-id="87594-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="87594-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="87594-127">**ScopeName**</span></span> |<span data-ttu-id="87594-128">hello hello 訂用帳戶、 資源群組或資源的名稱</span><span class="sxs-lookup"><span data-stu-id="87594-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="87594-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="87594-129">**ScopeType**</span></span> |<span data-ttu-id="87594-130">Hello 分派是否在 hello 訂用帳戶、 資源群組或資源範圍</span><span class="sxs-lookup"><span data-stu-id="87594-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="87594-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="87594-131">**Timestamp**</span></span> |<span data-ttu-id="87594-132">hello 日期和時間的存取權已變更</span><span class="sxs-lookup"><span data-stu-id="87594-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="87594-133">此範例命令會列出過去七天內 hello 訂用帳戶中的所有存取變更：</span><span class="sxs-lookup"><span data-stu-id="87594-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - 螢幕擷取畫面](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="87594-135">使用 Azure CLI 建立報告</span><span class="sxs-lookup"><span data-stu-id="87594-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="87594-136">toocreate hello Azure 命令列介面 (CLI)，以存取變更歷程記錄報表使用 hello`azure role assignment changelog list`命令。</span><span class="sxs-lookup"><span data-stu-id="87594-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="87594-137">匯出 tooa 試算表</span><span class="sxs-lookup"><span data-stu-id="87594-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="87594-138">toosave hello 報表，或操作 hello 資料、 匯出 hello 存取變成.csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="87594-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="87594-139">然後，您就可以檢視試算表中檢視 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="87594-139">You can then view hello report in a spreadsheet for review.</span></span>

![以試算表形式來檢視的變更記錄 - 螢幕擷取畫面](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="87594-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87594-141">Next steps</span></span>
* <span data-ttu-id="87594-142">使用 [Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="87594-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="87594-143">深入了解如何 toomanage [Azure rbac 進行使用 powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="87594-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

