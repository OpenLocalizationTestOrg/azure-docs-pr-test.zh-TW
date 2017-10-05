---
title: "如何在 Azure API 管理中使用角色型存取控制 | Microsoft Docs"
description: "了解如何在 Azure API 管理中使用內建角色和建立自訂角色"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: fa757a591d788f52d759bc24accedd3c55149ae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-role-based-access-control-in-azure-api-management"></a><span data-ttu-id="e99b5-103">如何在 Azure API 管理中使用角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="e99b5-103">How to Use Role-Based Access Control in Azure API Management</span></span>
<span data-ttu-id="e99b5-104">Azure API 管理需要 Azure 角色型存取控制 (RBAC) 才能針對 API 管理服務及實體 (例如 API、原則) 啟用細部存取管理。</span><span class="sxs-lookup"><span data-stu-id="e99b5-104">Azure API Management relies on Azure Role-Based Access Control (RBAC) to enable fine-grained access management for API Management services and entities (e.g., APIs, policies).</span></span> <span data-ttu-id="e99b5-105">本文章將為您提供 API 管理中內建角色和自訂角色的概觀。</span><span class="sxs-lookup"><span data-stu-id="e99b5-105">This article gives you an overview of the built-in and custom roles in API Management.</span></span> <span data-ttu-id="e99b5-106">如果您要深入了解 Azure 入口網站中的存取管理，請參閱[開始在 Azure 入口網站中使用存取管理](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)</span><span class="sxs-lookup"><span data-stu-id="e99b5-106">If you want more details on access management in the Azure portal, see [Get started with access management in the Azure portal](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)</span></span>

## <a name="built-in-roles"></a><span data-ttu-id="e99b5-107">內建角色</span><span class="sxs-lookup"><span data-stu-id="e99b5-107">Built-in Roles</span></span>
<span data-ttu-id="e99b5-108">API 管理目前提供 3 個內建角色，並將在不久的將來再新增 2 個角色。</span><span class="sxs-lookup"><span data-stu-id="e99b5-108">API Management currently provides 3 built-in roles and will add 2 more roles in the near future.</span></span> <span data-ttu-id="e99b5-109">這些角色可以指派到不同的範圍，包括訂用帳戶、資源群組，以及個別 API 管理執行個體。</span><span class="sxs-lookup"><span data-stu-id="e99b5-109">These roles can be assigned at differnt scopes including subscription, resource group, and individual API Management instance.</span></span> <span data-ttu-id="e99b5-110">例如，假設「Azure API 管理服務讀者」角色指派給資源群組層級的使用者，則該使用者會有該資源群組內所有 API 管理執行個體的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="e99b5-110">For instance, if the "Azure API Management Service Reader" role is assigned to an user at the resource group level, then the user will have read access to all API Management instances inside the resource group.</span></span> 

<span data-ttu-id="e99b5-111">下表提供內建角色的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="e99b5-111">The following table provides brief descriptions of the built-in roles.</span></span> <span data-ttu-id="e99b5-112">您可以使用 Azure 入口網站或其他工具 (包括 Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell)、Azure [命令列介面](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli)和 [REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest)) 指派這些角色。</span><span class="sxs-lookup"><span data-stu-id="e99b5-112">You can assign these roles using the Azure Portal or other tools including Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [Command-line interface](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), and [REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest).</span></span> <span data-ttu-id="e99b5-113">如需如何指派內建角色的詳細資料，請參閱[使用角色指派來管理 Azure 訂用帳戶資源的存取權](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)。</span><span class="sxs-lookup"><span data-stu-id="e99b5-113">For details about how to assign built-in roles, see [Use role assignments to manage access to your Azure subscription resources](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).</span></span>

| <span data-ttu-id="e99b5-114">角色</span><span class="sxs-lookup"><span data-stu-id="e99b5-114">Role</span></span>          | <span data-ttu-id="e99b5-115">讀取權限<sup>[1]</sup></span><span class="sxs-lookup"><span data-stu-id="e99b5-115">Read access<sup>[1]</sup></span></span> | <span data-ttu-id="e99b5-116">寫入權限<sup>[2]</sup></span><span class="sxs-lookup"><span data-stu-id="e99b5-116">Write access<sup>[2]</sup></span></span> | <span data-ttu-id="e99b5-117">服務建立、刪除、調整，VPN 及自訂網域設定</span><span class="sxs-lookup"><span data-stu-id="e99b5-117">Service creation, deletion, scaling, VPN and custom domain configuration</span></span> | <span data-ttu-id="e99b5-118">存取舊版發行者入口網站</span><span class="sxs-lookup"><span data-stu-id="e99b5-118">Access to legacy Publsiher Portal</span></span> | <span data-ttu-id="e99b5-119">說明</span><span class="sxs-lookup"><span data-stu-id="e99b5-119">Description</span></span>
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| <span data-ttu-id="e99b5-120">Azure API 管理服務參與者</span><span class="sxs-lookup"><span data-stu-id="e99b5-120">Azure API Management Service Contributor</span></span> | <span data-ttu-id="e99b5-121">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-121">✓</span></span> | <span data-ttu-id="e99b5-122">✓ </span><span class="sxs-lookup"><span data-stu-id="e99b5-122">✓</span></span> | <span data-ttu-id="e99b5-123">✓ </span><span class="sxs-lookup"><span data-stu-id="e99b5-123">✓</span></span> | <span data-ttu-id="e99b5-124">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-124">✓</span></span> | <span data-ttu-id="e99b5-125">進階使用者。</span><span class="sxs-lookup"><span data-stu-id="e99b5-125">Super user.</span></span> <span data-ttu-id="e99b5-126">具有 API 管理服務及實體 (例如 API、原則) 的完整 CRUD 存取權限。</span><span class="sxs-lookup"><span data-stu-id="e99b5-126">Has full CRUD access to API Management services and entities (e.g., APIs, Policies).</span></span> <span data-ttu-id="e99b5-127">具有舊版發行者入口網站的存取權限。</span><span class="sxs-lookup"><span data-stu-id="e99b5-127">Has access to the legacy publisher portal.</span></span> |
| <span data-ttu-id="e99b5-128">Azure API 管理服務讀者</span><span class="sxs-lookup"><span data-stu-id="e99b5-128">Azure API Management Service Reader</span></span> | <span data-ttu-id="e99b5-129">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-129">✓</span></span> | | || <span data-ttu-id="e99b5-130">具有 API 管理服務及實體的唯讀權限。</span><span class="sxs-lookup"><span data-stu-id="e99b5-130">Has read-only access to API Management services and entities.</span></span> |
| <span data-ttu-id="e99b5-131">Azure API 管理服務操作員</span><span class="sxs-lookup"><span data-stu-id="e99b5-131">Azure API Management Service Operator</span></span> | <span data-ttu-id="e99b5-132">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-132">✓</span></span> | | <span data-ttu-id="e99b5-133">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-133">✓</span></span> | | <span data-ttu-id="e99b5-134">可以管理 API 管理服務，但無法管理實體。</span><span class="sxs-lookup"><span data-stu-id="e99b5-134">Can manage API Management services but not entities.</span></span>|
| <span data-ttu-id="e99b5-135">Azure API 管理服務編輯者<sup>*</sup></span><span class="sxs-lookup"><span data-stu-id="e99b5-135">Azure API Management Service Editor<sup>*</sup></span></span> | <span data-ttu-id="e99b5-136">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-136">✓</span></span> | <span data-ttu-id="e99b5-137">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-137">✓</span></span> | |  | <span data-ttu-id="e99b5-138">可以管理 API 管理實體，但無法管理服務。</span><span class="sxs-lookup"><span data-stu-id="e99b5-138">Can manage API Management entities but not services.</span></span>|
| <span data-ttu-id="e99b5-139">Azure API 管理內容管理員<sup>*</sup></span><span class="sxs-lookup"><span data-stu-id="e99b5-139">Azure API Management Content Manager<sup>*</sup></span></span> | <span data-ttu-id="e99b5-140">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-140">✓</span></span> | | | <span data-ttu-id="e99b5-141">✓</span><span class="sxs-lookup"><span data-stu-id="e99b5-141">✓</span></span> | <span data-ttu-id="e99b5-142">可以管理開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="e99b5-142">Can manage developer portal.</span></span> <span data-ttu-id="e99b5-143">具有服務和實體的唯讀權限。</span><span class="sxs-lookup"><span data-stu-id="e99b5-143">Read-only access to services and entities.</span></span>|

<span data-ttu-id="e99b5-144"><sup>[1] API 管理服務及實體 (例如 API、原則) 的讀取權限</sup></span><span class="sxs-lookup"><span data-stu-id="e99b5-144"><sup>[1] Read access to API Management services and entities (e.g., APIs, policies)</sup></span></span>

<span data-ttu-id="e99b5-145"><sup>[2] API 管理服務及實體的寫入權限，下列作業除外：1) 建立、刪除和調整執行個體 2) VPN 組態  3) 自訂網域名稱設定</sup></span><span class="sxs-lookup"><span data-stu-id="e99b5-145"><sup>[2] Write access to API Management services and entities except following opeartions: 1) Instance creation, deletion, and scaling 2) VPN configuration  3) Custom domain name setup</sup></span></span>

<span data-ttu-id="e99b5-146"><sup>\* 當我們將現有發行者入口網站的所有系統管理 UI 移轉至 Azure 入口網站後，將會提供「服務編輯者」角色。在發行者入口網站重構為僅包含管理開發人員入口網站的相關功能之後，將會提供「內容管理者」角色。</sup></span><span class="sxs-lookup"><span data-stu-id="e99b5-146"><sup>\* The Service Editor role will be available after we migrate all admin UI from the existing publisher portal to the Azure portal. The Content Manager role will be available after the publisher portal is refactored to only contain functionalities related to managing the developer portal.</sup></span></span>  


## <a name="custom-roles"></a><span data-ttu-id="e99b5-147">自訂角色</span><span class="sxs-lookup"><span data-stu-id="e99b5-147">Custom Roles</span></span>
<span data-ttu-id="e99b5-148">如果內建角色都無法滿足您的特定需求，您可以建立自訂角色來提供更精細的 API 管理實體存取管理。</span><span class="sxs-lookup"><span data-stu-id="e99b5-148">If none of the built-in roles meet your specific needs, custom roles can be created to provide more granular access management for API Management entities.</span></span> <span data-ttu-id="e99b5-149">例如，您可以建立自訂角色，使其具有 API 管理服務的唯讀權限，但只有單一特定 API 的寫入權限。</span><span class="sxs-lookup"><span data-stu-id="e99b5-149">For example, you can create a custom role which has read-only access to an API Management service but only has write access to one specific API.</span></span> <span data-ttu-id="e99b5-150">若要深入了解自訂角色，請參閱 [Azure RBAC 中的自訂角色](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)。</span><span class="sxs-lookup"><span data-stu-id="e99b5-150">To learn more details about custom roles, see [Custom Roles in Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles).</span></span> 

<span data-ttu-id="e99b5-151">當您建立自訂角色時，從其中一個內建角色開始會比較輕鬆。</span><span class="sxs-lookup"><span data-stu-id="e99b5-151">When you create a custom role, it is easier to start with one of the built-in roles.</span></span> <span data-ttu-id="e99b5-152">編輯屬性來加入 Actions、NotActions 或 AssignableScopes，然後將變更另存為新角色。</span><span class="sxs-lookup"><span data-stu-id="e99b5-152">Edit the attributes to add the Actions, NotActions, or AssignableScopes, then save the changes as a new role.</span></span> <span data-ttu-id="e99b5-153">以下範例從「Azure API 管理服務讀者」角色開始，建立一個名為「計算機 API 編輯者」的自訂角色。</span><span class="sxs-lookup"><span data-stu-id="e99b5-153">The following example begins with the "Azure API Managment Service Reader" role and creates a custom role called "Calculator API Editor".</span></span> <span data-ttu-id="e99b5-154">自訂角色可以只指派給特定 API，如此就只能存取該 API。</span><span class="sxs-lookup"><span data-stu-id="e99b5-154">The custom role can be assigned only to a specific API therefore will only has access to that API.</span></span> 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access to Contoso APIM instance and write access to the Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of the user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a><span data-ttu-id="e99b5-155">觀看影片概觀</span><span class="sxs-lookup"><span data-stu-id="e99b5-155">Watch a Video Overview</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e99b5-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e99b5-156">Next Steps</span></span>

* <span data-ttu-id="e99b5-157">深入了解 Azure 中的角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="e99b5-157">Learn more about Role-Based Access Control in Azure</span></span>
  * [<span data-ttu-id="e99b5-158">開始在 Azure 入口網站中使用存取管理</span><span class="sxs-lookup"><span data-stu-id="e99b5-158">Get started with access management in the Azure portal</span></span>](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [<span data-ttu-id="e99b5-159">使用角色指派來管理 Azure 訂用帳戶資源的存取權</span><span class="sxs-lookup"><span data-stu-id="e99b5-159">Use role assignments to manage access to your Azure subscription resources</span></span>](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [<span data-ttu-id="e99b5-160">Azure RBAC 中的自訂角色</span><span class="sxs-lookup"><span data-stu-id="e99b5-160">Custom Roles in Azure RBAC</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
