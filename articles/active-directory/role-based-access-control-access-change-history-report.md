---
title: "存取報告 - Azure RBAC | Microsoft Docs"
description: "產生一份報告，其中列出您的 Azure 訂用帳戶 (採用角色型存取控制) 在過去 90 天內的所有存取權變更。"
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
ms.openlocfilehash: 4e8028ab43ed02ef0c0a1374326b07f72f97d9d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="e3c28-103">建立角色型存取控制的存取報告</span><span class="sxs-lookup"><span data-stu-id="e3c28-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="e3c28-104">每當有人授與或撤銷您訂用帳戶中的存取權時，變更就會記錄在 Azure 事件中。</span><span class="sxs-lookup"><span data-stu-id="e3c28-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span></span> <span data-ttu-id="e3c28-105">您可以建立存取權變更歷程記錄報告，以查看過去 90 天內的所有變更。</span><span class="sxs-lookup"><span data-stu-id="e3c28-105">You can create access change history reports to see all changes for the past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="e3c28-106">使用 Azure PowerShell 建立報告</span><span class="sxs-lookup"><span data-stu-id="e3c28-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="e3c28-107">若要在 PowerShell 中建立存取權變更歷程記錄報告，請使用 [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) 命令。</span><span class="sxs-lookup"><span data-stu-id="e3c28-107">To create an access change history report in PowerShell, use the [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="e3c28-108">呼叫此命令時，您可以指定要列出哪一個指派屬性，其中包括下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="e3c28-108">When you call this command, you can specify which property of the assignments you want listed, including the following:</span></span>

| <span data-ttu-id="e3c28-109">屬性</span><span class="sxs-lookup"><span data-stu-id="e3c28-109">Property</span></span> | <span data-ttu-id="e3c28-110">說明</span><span class="sxs-lookup"><span data-stu-id="e3c28-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3c28-111">**Action**</span><span class="sxs-lookup"><span data-stu-id="e3c28-111">**Action**</span></span> |<span data-ttu-id="e3c28-112">已授與或已撤銷存取權</span><span class="sxs-lookup"><span data-stu-id="e3c28-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="e3c28-113">**Caller**</span><span class="sxs-lookup"><span data-stu-id="e3c28-113">**Caller**</span></span> |<span data-ttu-id="e3c28-114">負責存取權變更的擁有者</span><span class="sxs-lookup"><span data-stu-id="e3c28-114">The owner responsible for the access change</span></span> |
| <span data-ttu-id="e3c28-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="e3c28-115">**PrincipalId**</span></span> | <span data-ttu-id="e3c28-116">已指派角色之使用者、群組或應用程式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e3c28-116">The unique identifier of the user, group, or application that was assigned the role</span></span> |
| <span data-ttu-id="e3c28-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="e3c28-117">**PrincipalName**</span></span> |<span data-ttu-id="e3c28-118">使用者、群組或應用程式的名稱</span><span class="sxs-lookup"><span data-stu-id="e3c28-118">The name of the user, group, or application</span></span> |
| <span data-ttu-id="e3c28-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="e3c28-119">**PrincipalType**</span></span> |<span data-ttu-id="e3c28-120">指派對象為使用者、群組或應用程式</span><span class="sxs-lookup"><span data-stu-id="e3c28-120">Whether the assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="e3c28-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="e3c28-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="e3c28-122">已授與或已撤銷之角色的 GUID</span><span class="sxs-lookup"><span data-stu-id="e3c28-122">The GUID of the role that was granted or revoked</span></span> |
| <span data-ttu-id="e3c28-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="e3c28-123">**RoleName**</span></span> |<span data-ttu-id="e3c28-124">已授與或已撤銷的角色</span><span class="sxs-lookup"><span data-stu-id="e3c28-124">The role that was granted or revoked</span></span> |
| <span data-ttu-id="e3c28-125">**範圍**</span><span class="sxs-lookup"><span data-stu-id="e3c28-125">**Scope**</span></span> | <span data-ttu-id="e3c28-126">套用指派之訂用帳戶、資源群組或資源的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e3c28-126">The unique identifier of the subscription, resource group, or resource that the assignment applies to</span></span> | 
| <span data-ttu-id="e3c28-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="e3c28-127">**ScopeName**</span></span> |<span data-ttu-id="e3c28-128">訂用帳戶、資源群組或資源的名稱</span><span class="sxs-lookup"><span data-stu-id="e3c28-128">The name of the subscription, resource group, or resource</span></span> |
| <span data-ttu-id="e3c28-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="e3c28-129">**ScopeType**</span></span> |<span data-ttu-id="e3c28-130">指派的範圍是訂用帳戶、資源群組或資源</span><span class="sxs-lookup"><span data-stu-id="e3c28-130">Whether the assignment was at the subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="e3c28-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="e3c28-131">**Timestamp**</span></span> |<span data-ttu-id="e3c28-132">變更存取權的日期和時間</span><span class="sxs-lookup"><span data-stu-id="e3c28-132">The date and time that access was changed</span></span> |

<span data-ttu-id="e3c28-133">此範例命令會列出過去 7 天訂用帳戶中的所有存取權變更：</span><span class="sxs-lookup"><span data-stu-id="e3c28-133">This example command lists all access changes in the subscription for the past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - 螢幕擷取畫面](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="e3c28-135">使用 Azure CLI 建立報告</span><span class="sxs-lookup"><span data-stu-id="e3c28-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="e3c28-136">若要在 Azure 命令列介面 (CLI) 中建立存取權變更歷程記錄報告，請使用 `azure role assignment changelog list` 命令。</span><span class="sxs-lookup"><span data-stu-id="e3c28-136">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span></span>

## <a name="export-to-a-spreadsheet"></a><span data-ttu-id="e3c28-137">匯出為試算表</span><span class="sxs-lookup"><span data-stu-id="e3c28-137">Export to a spreadsheet</span></span>
<span data-ttu-id="e3c28-138">若要儲存報告或處理此資料，請將存取權變更匯出為 .csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="e3c28-138">To save the report, or manipulate the data, export the access changes into a .csv file.</span></span> <span data-ttu-id="e3c28-139">您即可在試算表中檢閱此報告。</span><span class="sxs-lookup"><span data-stu-id="e3c28-139">You can then view the report in a spreadsheet for review.</span></span>

![以試算表形式來檢視的變更記錄 - 螢幕擷取畫面](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="e3c28-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3c28-141">Next steps</span></span>
* <span data-ttu-id="e3c28-142">使用 [Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="e3c28-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="e3c28-143">了解如何[使用 PowerShell 管理 Azure RBAC](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e3c28-143">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

