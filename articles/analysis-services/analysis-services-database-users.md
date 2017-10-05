---
title: "管理 Azure Analysis Services 中的使用者角色和使用者 | Microsoft Docs"
description: "了解如何在 Azure 中管理 Analysis Services 伺服器上的資料庫角色和使用者。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: d0bc7d7514f111b4bbde33bd60ae21264bd797fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="cb5c6-103">管理資料庫角色和使用者</span><span class="sxs-lookup"><span data-stu-id="cb5c6-103">Manage database roles and users</span></span>

<span data-ttu-id="cb5c6-104">在模型資料庫層級上，所有使用者都必須屬於某個角色。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="cb5c6-105">角色可針對模型資料庫定義具有特定權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="cb5c6-106">任何新增至某個角色的使用者或安全性群組都必須在與伺服器相同的訂用帳戶中具有 Azure AD 租用戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span>

<span data-ttu-id="cb5c6-107">定義角色的方式會根據您使用的工具而有所不同，但效果一樣。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="cb5c6-108">角色權限包括：</span><span class="sxs-lookup"><span data-stu-id="cb5c6-108">Role permissions include:</span></span>
*  <span data-ttu-id="cb5c6-109">**系統管理員** - 使用者具有資料庫的完整權限。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="cb5c6-110">具有系統管理員權限的資料庫角色與伺服器管理員不同。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="cb5c6-111">**處理** - 使用者可以連線到資料庫並對其執行處理作業，以及分析模型資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="cb5c6-112">**讀取** - 使用者可以使用用戶端應用程式來連接和分析模型資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="cb5c6-113">建立表格式模型專案時，您可在 SSDT 中使用角色管理員來建立角色，並將使用者或群組新增至這些角色。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="cb5c6-114">若部署至伺服器，您可使用 SSMS、[Analysis Services PowerShell Cmdlet](https://msdn.microsoft.com/library/hh758425.aspx) 或[表格式模型指令碼語言](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL)，新增或移除角色和使用者成員。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="cb5c6-115">在 SSDT 中新增或管理角色和使用者</span><span class="sxs-lookup"><span data-stu-id="cb5c6-115">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="cb5c6-116">在 SSDT > [表格式模型總管] 中，以滑鼠右鍵按一下 [角色]。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="cb5c6-117">在 [角色管理員] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="cb5c6-118">輸入角色的名稱。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-118">Type a name for the role.</span></span>  
  
     <span data-ttu-id="cb5c6-119">根據預設，每個新角色的預設角色名稱是以累加方式編號。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-119">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="cb5c6-120">建議您輸入可清楚識別成員類型的名稱，例如「財務經理」或「人力資源專員」。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-120">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="cb5c6-121">選取下列其中一個權限：</span><span class="sxs-lookup"><span data-stu-id="cb5c6-121">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="cb5c6-122">權限</span><span class="sxs-lookup"><span data-stu-id="cb5c6-122">Permission</span></span>|<span data-ttu-id="cb5c6-123">說明</span><span class="sxs-lookup"><span data-stu-id="cb5c6-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="cb5c6-124">**None**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-124">**None**</span></span>|<span data-ttu-id="cb5c6-125">成員無法修改模型結構描述，也無法查詢資料。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-125">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="cb5c6-126">**讀取**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-126">**Read**</span></span>|<span data-ttu-id="cb5c6-127">成員可以查詢資料 (根據資料列篩選條件)，但無法修改模型結構描述。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-127">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="cb5c6-128">**讀取和處理**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-128">**Read and Process**</span></span>|<span data-ttu-id="cb5c6-129">成員可以查詢資料 (根據資料列層級的篩選條件)，並執行「處理」和「全部處理」作業，但無法修改模型結構描述。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="cb5c6-130">**處理程序**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-130">**Process**</span></span>|<span data-ttu-id="cb5c6-131">成員可以執行「處理」和「全部處理」作業。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="cb5c6-132">無法修改模型結構描述，也無法查詢資料。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-132">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="cb5c6-133">**系統管理員**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-133">**Administrator**</span></span>|<span data-ttu-id="cb5c6-134">成員可以修改模型結構描述及查詢所有資料。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-134">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="cb5c6-135">如果您建立的角色具有「讀取」或「讀取和處理」權限，您可以使用 DAX 公式來新增資料列篩選條件。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-135">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="cb5c6-136">按一下 [資料列篩選條件] 索引標籤，然後選取資料表，再按一下 [DAX 篩選條件] 欄位，然後輸入 DAX 公式。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-136">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="cb5c6-137">按一下 [成員] >  [新增外部]。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="cb5c6-138">在 [新增外部成員] 中，依照電子郵件地址輸入 Azure AD 租用戶中的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="cb5c6-139">按一下 [確定] 並關閉 [角色管理員] 後，角色和角色成員就會出現在 [表格式模型總管] 中。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![表格式模型總管中的角色和使用者](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="cb5c6-141">部署到 Azure Analysis Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-141">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="cb5c6-142">在 SSMS 中新增或管理角色和使用者</span><span class="sxs-lookup"><span data-stu-id="cb5c6-142">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="cb5c6-143">若要將角色和使用者新增至已部署的模型資料庫，您必須以伺服器管理員身分連線到伺服器，或已經是具有系統管理員權限的資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-143">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="cb5c6-144">在 [物件總館] 中，以滑鼠右鍵按一下 [角色] > [新增角色]。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="cb5c6-145">在 [建立角色] 中，輸入角色名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="cb5c6-146">選取權限。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-146">Select a permission.</span></span>
   |<span data-ttu-id="cb5c6-147">權限</span><span class="sxs-lookup"><span data-stu-id="cb5c6-147">Permission</span></span>|<span data-ttu-id="cb5c6-148">說明</span><span class="sxs-lookup"><span data-stu-id="cb5c6-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="cb5c6-149">**完全控制 (系統管理員)**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="cb5c6-150">成員可以修改模型結構描述、程序，以及查詢所有資料。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-150">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="cb5c6-151">**處理資料庫**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-151">**Process database**</span></span>|<span data-ttu-id="cb5c6-152">成員可以執行「處理」和「全部處理」作業。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="cb5c6-153">無法修改模型結構描述，也無法查詢資料。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-153">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="cb5c6-154">**讀取**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-154">**Read**</span></span>|<span data-ttu-id="cb5c6-155">成員可以查詢資料 (根據資料列篩選條件)，但無法修改模型結構描述。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-155">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="cb5c6-156">按一下 [成員資格]，然後依照電子郵件地址輸入 Azure AD 租用戶中的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![新增使用者](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="cb5c6-158">如果您建立的角色具有「讀取」權限，您可以使用 DAX 公式來新增資料列篩選條件。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-158">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="cb5c6-159">按一下 [資料列篩選條件]，選取資料表，然後在 [DAX 篩選條件] 欄位中輸入 DAX 公式。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-159">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="cb5c6-160">使用 TMSL 指令碼新增角色和使用者</span><span class="sxs-lookup"><span data-stu-id="cb5c6-160">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="cb5c6-161">您可以在 SSMS 中 或使用 PowerShell，在 XMLA 視窗中執行 TMSL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-161">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="cb5c6-162">使用 [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) 命令和 [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) 物件。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-162">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="cb5c6-163">**TMSL 指令碼範例**</span><span class="sxs-lookup"><span data-stu-id="cb5c6-163">**Sample TMSL script**</span></span>

<span data-ttu-id="cb5c6-164">在此範例中，B2B 外部使用者和群組會新增至 SalesBI 資料庫中具讀取權限的分析師角色。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-164">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="cb5c6-165">外部使用者和群組必須在相同的 Azure AD 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-165">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="cb5c6-166">使用 PowerShell 新增角色和使用者</span><span class="sxs-lookup"><span data-stu-id="cb5c6-166">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="cb5c6-167">[SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) 模組提供特定工作的資料庫管理 Cmdlet，以及可接受表格式模型指令碼語言 (TMSL) 查詢或指令碼的一般用途 Invoke-ASCmd Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-167">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="cb5c6-168">下列 Cmdlet 用來管理資料庫角色和使用者。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-168">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="cb5c6-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="cb5c6-169">Cmdlet</span></span>|<span data-ttu-id="cb5c6-170">說明</span><span class="sxs-lookup"><span data-stu-id="cb5c6-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="cb5c6-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="cb5c6-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="cb5c6-172">將成員新增到資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-172">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="cb5c6-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="cb5c6-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="cb5c6-174">從資料庫角色移除成員。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="cb5c6-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="cb5c6-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="cb5c6-176">執行 TMSL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="cb5c6-177">資料列篩選條件</span><span class="sxs-lookup"><span data-stu-id="cb5c6-177">Row filters</span></span>  
<span data-ttu-id="cb5c6-178">資料列篩選條件定義特定角色的成員可以查詢資料表中的哪些資料列。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="cb5c6-179">使用 DAX 公式，針對模型中的每個資料表定義資料列篩選條件。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="cb5c6-180">只能針對具有「讀取」和「讀取和處理」權限的角色定義資料列篩選條件。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="cb5c6-181">根據預設，如果未針對特定資料表定義資料列篩選條件，則成員可以查詢資料表中的所有資料列，除非從另一個資料表套用交叉篩選。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-181">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="cb5c6-182">資料列篩選條件需要 DAX 公式，其必須評估為 TRUE/FALSE 值，以定義該特定角色的成員可以查詢的資料列。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-182">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="cb5c6-183">無法查詢 DAX 公式中未包含的資料列。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-183">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="cb5c6-184">例如，具有資料列篩選條件運算式 (=Customers [Country] = “USA”) 的「客戶」資料表，「銷售」角色成員只能查看美國的客戶。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-184">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="cb5c6-185">資料列篩選條件會套用至指定的資料列和相關資料列。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-185">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="cb5c6-186">若資料表具有多個關聯性，篩選條件就會套用作用中關聯性的安全性。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-186">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="cb5c6-187">資料列篩選條件會與針對相關資料表定義的其他資料列篩選條件產生交集，例如：</span><span class="sxs-lookup"><span data-stu-id="cb5c6-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="cb5c6-188">資料表</span><span class="sxs-lookup"><span data-stu-id="cb5c6-188">Table</span></span>|<span data-ttu-id="cb5c6-189">DAX 運算式</span><span class="sxs-lookup"><span data-stu-id="cb5c6-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="cb5c6-190">區域</span><span class="sxs-lookup"><span data-stu-id="cb5c6-190">Region</span></span>|<span data-ttu-id="cb5c6-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="cb5c6-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="cb5c6-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="cb5c6-192">ProductCategory</span></span>|<span data-ttu-id="cb5c6-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="cb5c6-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="cb5c6-194">交易</span><span class="sxs-lookup"><span data-stu-id="cb5c6-194">Transactions</span></span>|<span data-ttu-id="cb5c6-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="cb5c6-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="cb5c6-196">淨效應是成員可以查詢客戶位於美國、產品類別為自行車且 2016 年之資料的資料列。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-196">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="cb5c6-197">使用者無法查詢美國以外的交易、非自行車的交易或不在 2016 年的交易，除非他們是授與這些權限之另一個角色的成員。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-197">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="cb5c6-198">您可以使用 =FALSE() 篩選條件，拒絕存取整個資料表的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="cb5c6-198">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb5c6-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb5c6-199">Next steps</span></span>
  <span data-ttu-id="cb5c6-200">[管理伺服器管理員](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="cb5c6-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="cb5c6-201">使用 PowerShell 管理 Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb5c6-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="cb5c6-202">表格式模型指令碼語言 (TMSL) 參考</span><span class="sxs-lookup"><span data-stu-id="cb5c6-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

