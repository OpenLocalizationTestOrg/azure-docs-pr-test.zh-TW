---
title: "aaaManage 資料庫角色和 Azure Analysis Services 中的使用者 |Microsoft 文件"
description: "了解如何 toomanage 資料庫角色和 Azure 中的 Analysis Services 伺服器上的使用者。"
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
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="e55c1-103">管理資料庫角色和使用者</span><span class="sxs-lookup"><span data-stu-id="e55c1-103">Manage database roles and users</span></span>

<span data-ttu-id="e55c1-104">資料庫層級 hello 模型，所有使用者必須都屬於 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="e55c1-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="e55c1-105">角色定義與 hello 模型資料庫的特定權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="e55c1-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="e55c1-106">任何使用者或安全性群組新增 tooa 角色必須有在 hello Azure AD 租用戶的帳戶相同的訂用帳戶與 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e55c1-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="e55c1-107">您如何定義角色是不同視 hello 工具使用，但 hello 效果是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="e55c1-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="e55c1-108">角色權限包括：</span><span class="sxs-lookup"><span data-stu-id="e55c1-108">Role permissions include:</span></span>
*  <span data-ttu-id="e55c1-109">**系統管理員**位使用者擁有 hello 資料庫的完整權限。</span><span class="sxs-lookup"><span data-stu-id="e55c1-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="e55c1-110">具有系統管理員權限的資料庫角色與伺服器管理員不同。</span><span class="sxs-lookup"><span data-stu-id="e55c1-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="e55c1-111">**處理序**-使用者可以連線 tooand 執行 hello 資料庫上的處理作業和分析模型資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="e55c1-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="e55c1-112">**讀取**-使用者可以使用用戶端應用程式 tooconnect tooand 分析模型資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="e55c1-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="e55c1-113">建立表格式模型專案時，您會建立角色，並在 SSDT 中使用角色管理員新增使用者或群組 toothose 角色。</span><span class="sxs-lookup"><span data-stu-id="e55c1-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="e55c1-114">當部署的 tooa 伺服器，您使用 SSMS， [Analysis Services PowerShell 指令程式](https://msdn.microsoft.com/library/hh758425.aspx)，或[表格式模型指令碼語言](https://msdn.microsoft.com/library/mt614797.aspx)(TMSL) tooadd 或移除角色和使用者的成員。</span><span class="sxs-lookup"><span data-stu-id="e55c1-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="e55c1-115">tooadd 或管理角色和在 SSDT 中的使用者</span><span class="sxs-lookup"><span data-stu-id="e55c1-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="e55c1-116">在 SSDT > [表格式模型總管] 中，以滑鼠右鍵按一下 [角色]。</span><span class="sxs-lookup"><span data-stu-id="e55c1-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="e55c1-117">在 [角色管理員] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e55c1-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="e55c1-118">輸入 hello 角色的名稱。</span><span class="sxs-lookup"><span data-stu-id="e55c1-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="e55c1-119">根據預設，hello hello 預設角色名稱是以累加方式編號為每個新的角色。</span><span class="sxs-lookup"><span data-stu-id="e55c1-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="e55c1-120">建議您輸入清楚識別 hello 成員類型，例如 「 財務經理 」 或 「 人力資源專員的名稱。</span><span class="sxs-lookup"><span data-stu-id="e55c1-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="e55c1-121">選取其中一個 hello 下列權限：</span><span class="sxs-lookup"><span data-stu-id="e55c1-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="e55c1-122">權限</span><span class="sxs-lookup"><span data-stu-id="e55c1-122">Permission</span></span>|<span data-ttu-id="e55c1-123">說明</span><span class="sxs-lookup"><span data-stu-id="e55c1-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="e55c1-124">**None**</span><span class="sxs-lookup"><span data-stu-id="e55c1-124">**None**</span></span>|<span data-ttu-id="e55c1-125">成員無法修改 hello 模型結構描述，且無法查詢資料。</span><span class="sxs-lookup"><span data-stu-id="e55c1-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="e55c1-126">**讀取**</span><span class="sxs-lookup"><span data-stu-id="e55c1-126">**Read**</span></span>|<span data-ttu-id="e55c1-127">成員可以查詢資料 （根據資料列篩選），但無法修改 hello 模型結構描述。</span><span class="sxs-lookup"><span data-stu-id="e55c1-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="e55c1-128">**讀取和處理**</span><span class="sxs-lookup"><span data-stu-id="e55c1-128">**Read and Process**</span></span>|<span data-ttu-id="e55c1-129">成員可以查詢資料 （根據資料列層級篩選） 和執行的處理 」 和 「 處理全部作業，但無法修改 hello 模型結構描述。</span><span class="sxs-lookup"><span data-stu-id="e55c1-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="e55c1-130">**處理程序**</span><span class="sxs-lookup"><span data-stu-id="e55c1-130">**Process**</span></span>|<span data-ttu-id="e55c1-131">成員可以執行「處理」和「全部處理」作業。</span><span class="sxs-lookup"><span data-stu-id="e55c1-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="e55c1-132">無法修改 hello 模型結構描述，也無法查詢資料。</span><span class="sxs-lookup"><span data-stu-id="e55c1-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="e55c1-133">**系統管理員**</span><span class="sxs-lookup"><span data-stu-id="e55c1-133">**Administrator**</span></span>|<span data-ttu-id="e55c1-134">成員可以修改 hello 模型結構描述，並查詢所有資料。</span><span class="sxs-lookup"><span data-stu-id="e55c1-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="e55c1-135">如果您是 hello 角色建立具有讀取或讀取和處理序的權限，您可以透過使用 DAX 公式加入資料列篩選。</span><span class="sxs-lookup"><span data-stu-id="e55c1-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="e55c1-136">按一下 hello**資料列篩選器**索引標籤，然後選取資料表，再按一下 hello **DAX 篩選**欄位，並輸入 DAX 公式。</span><span class="sxs-lookup"><span data-stu-id="e55c1-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="e55c1-137">按一下 [成員] >  [新增外部]。</span><span class="sxs-lookup"><span data-stu-id="e55c1-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="e55c1-138">在 [新增外部成員] 中，依照電子郵件地址輸入 Azure AD 租用戶中的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="e55c1-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="e55c1-139">按一下 [確定] 並關閉 [角色管理員] 後，角色和角色成員就會出現在 [表格式模型總管] 中。</span><span class="sxs-lookup"><span data-stu-id="e55c1-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![表格式模型總管中的角色和使用者](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="e55c1-141">部署 tooyour Azure Analysis Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e55c1-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="e55c1-142">tooadd 或管理角色和在 SSMS 中的使用者</span><span class="sxs-lookup"><span data-stu-id="e55c1-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="e55c1-143">tooadd 角色和使用者 tooa 部署模型資料庫，您必須是伺服器連接的 toohello 伺服器系統管理員身分或已經是系統管理員權限的資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="e55c1-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="e55c1-144">在 [物件總館] 中，以滑鼠右鍵按一下 [角色] > [新增角色]。</span><span class="sxs-lookup"><span data-stu-id="e55c1-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="e55c1-145">在 [建立角色] 中，輸入角色名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="e55c1-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="e55c1-146">選取權限。</span><span class="sxs-lookup"><span data-stu-id="e55c1-146">Select a permission.</span></span>
   |<span data-ttu-id="e55c1-147">權限</span><span class="sxs-lookup"><span data-stu-id="e55c1-147">Permission</span></span>|<span data-ttu-id="e55c1-148">說明</span><span class="sxs-lookup"><span data-stu-id="e55c1-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="e55c1-149">**完全控制 (系統管理員)**</span><span class="sxs-lookup"><span data-stu-id="e55c1-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="e55c1-150">成員可以修改 hello 模型結構描述中，處理，以及查詢的所有資料。</span><span class="sxs-lookup"><span data-stu-id="e55c1-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="e55c1-151">**處理資料庫**</span><span class="sxs-lookup"><span data-stu-id="e55c1-151">**Process database**</span></span>|<span data-ttu-id="e55c1-152">成員可以執行「處理」和「全部處理」作業。</span><span class="sxs-lookup"><span data-stu-id="e55c1-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="e55c1-153">無法修改 hello 模型結構描述，也無法查詢資料。</span><span class="sxs-lookup"><span data-stu-id="e55c1-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="e55c1-154">**讀取**</span><span class="sxs-lookup"><span data-stu-id="e55c1-154">**Read**</span></span>|<span data-ttu-id="e55c1-155">成員可以查詢資料 （根據資料列篩選），但無法修改 hello 模型結構描述。</span><span class="sxs-lookup"><span data-stu-id="e55c1-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="e55c1-156">按一下 [成員資格]，然後依照電子郵件地址輸入 Azure AD 租用戶中的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="e55c1-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![新增使用者](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="e55c1-158">如果您要建立 hello 角色具有讀取權限，您可以透過使用 DAX 公式加入資料列篩選。</span><span class="sxs-lookup"><span data-stu-id="e55c1-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="e55c1-159">按一下**資料列篩選器**選取資料表，然後輸入 DAX 公式在 hello **DAX 篩選**欄位。</span><span class="sxs-lookup"><span data-stu-id="e55c1-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="e55c1-160">tooadd 角色和使用者使用 TMSL 指令碼</span><span class="sxs-lookup"><span data-stu-id="e55c1-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="e55c1-161">您可以在 SSMS 中，或使用 PowerShell 的 hello 的 XMLA 視窗中執行 TMSL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e55c1-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="e55c1-162">使用 hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl)命令和 hello[角色](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl)物件。</span><span class="sxs-lookup"><span data-stu-id="e55c1-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="e55c1-163">**TMSL 指令碼範例**</span><span class="sxs-lookup"><span data-stu-id="e55c1-163">**Sample TMSL script**</span></span>

<span data-ttu-id="e55c1-164">在此範例中，B2B 外部的使用者和群組會加入 toohello 分析師角色擁有 hello SalesBI 資料庫的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="e55c1-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="e55c1-165">同時 hello 外部使用者和群組必須在同一個租用戶的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="e55c1-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
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

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="e55c1-166">tooadd 角色和使用者使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e55c1-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="e55c1-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx)模組提供的工作特有的資料庫管理 cmdlet 和 hello 一般用途 Invoke-ascmd 指令程式可接受表格式模型指令碼語言 (TMSL) 查詢或指令碼。</span><span class="sxs-lookup"><span data-stu-id="e55c1-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="e55c1-168">hello 下列 cmdlet 可用來管理資料庫角色和使用者。</span><span class="sxs-lookup"><span data-stu-id="e55c1-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="e55c1-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e55c1-169">Cmdlet</span></span>|<span data-ttu-id="e55c1-170">說明</span><span class="sxs-lookup"><span data-stu-id="e55c1-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="e55c1-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="e55c1-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="e55c1-172">加入成員 tooa 資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="e55c1-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="e55c1-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="e55c1-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="e55c1-174">從資料庫角色移除成員。</span><span class="sxs-lookup"><span data-stu-id="e55c1-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="e55c1-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="e55c1-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="e55c1-176">執行 TMSL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e55c1-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="e55c1-177">資料列篩選條件</span><span class="sxs-lookup"><span data-stu-id="e55c1-177">Row filters</span></span>  
<span data-ttu-id="e55c1-178">資料列篩選條件定義特定角色的成員可以查詢資料表中的哪些資料列。</span><span class="sxs-lookup"><span data-stu-id="e55c1-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="e55c1-179">使用 DAX 公式，針對模型中的每個資料表定義資料列篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e55c1-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="e55c1-180">只能針對具有「讀取」和「讀取和處理」權限的角色定義資料列篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e55c1-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="e55c1-181">根據預設，如果資料列篩選器沒有定義特定資料表中，成員可以查詢 hello 資料表中的所有資料列除非從另一個資料表套用交叉篩選。</span><span class="sxs-lookup"><span data-stu-id="e55c1-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="e55c1-182">資料列篩選器需要 DAX 公式，必須評估 tooa TRUE/FALSE 值，該特定角色的成員可以查詢 toodefine hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="e55c1-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="e55c1-183">無法查詢未包含在 hello DAX 公式的資料列。</span><span class="sxs-lookup"><span data-stu-id="e55c1-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="e55c1-184">例如，下列資料列篩選器運算式，hello 與 hello Customers 資料表*= 客戶 [Country] ="USA"*，hello 銷售 」 角色的成員只能看到 hello 美國的客戶。</span><span class="sxs-lookup"><span data-stu-id="e55c1-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="e55c1-185">資料列篩選器套用 toohello 指定資料列和相關的資料列。</span><span class="sxs-lookup"><span data-stu-id="e55c1-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="e55c1-186">當資料表具有多個關聯性時，篩選會套用安全性為使用中的 hello 關聯性。</span><span class="sxs-lookup"><span data-stu-id="e55c1-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="e55c1-187">資料列篩選條件會與針對相關資料表定義的其他資料列篩選條件產生交集，例如：</span><span class="sxs-lookup"><span data-stu-id="e55c1-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="e55c1-188">資料表</span><span class="sxs-lookup"><span data-stu-id="e55c1-188">Table</span></span>|<span data-ttu-id="e55c1-189">DAX 運算式</span><span class="sxs-lookup"><span data-stu-id="e55c1-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="e55c1-190">區域</span><span class="sxs-lookup"><span data-stu-id="e55c1-190">Region</span></span>|<span data-ttu-id="e55c1-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="e55c1-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="e55c1-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="e55c1-192">ProductCategory</span></span>|<span data-ttu-id="e55c1-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="e55c1-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="e55c1-194">交易</span><span class="sxs-lookup"><span data-stu-id="e55c1-194">Transactions</span></span>|<span data-ttu-id="e55c1-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="e55c1-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="e55c1-196">hello 最後的結果是成員可以查詢其中 hello 客戶位於 hello 美國、 hello 產品類別目錄是自行車，而 hello 年份是 2016年的資料列。</span><span class="sxs-lookup"><span data-stu-id="e55c1-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="e55c1-197">使用者無法查詢交易的交易之外 hello USA 不自行車或交易中所沒有 2016年除非授與這些權限的另一個角色的成員。</span><span class="sxs-lookup"><span data-stu-id="e55c1-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="e55c1-198">您可以使用 hello 篩選*=FALSE()*，toodeny 存取 tooall 資料列，針對整個資料表。</span><span class="sxs-lookup"><span data-stu-id="e55c1-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e55c1-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e55c1-199">Next steps</span></span>
  <span data-ttu-id="e55c1-200">[管理伺服器管理員](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="e55c1-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="e55c1-201">使用 PowerShell 管理 Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e55c1-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="e55c1-202">表格式模型指令碼語言 (TMSL) 參考</span><span class="sxs-lookup"><span data-stu-id="e55c1-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

