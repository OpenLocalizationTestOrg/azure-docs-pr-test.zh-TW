---
title: "在 Azure Active Directory 中還原已刪除的 Office 365 群組 | Microsoft Docs"
description: "如何還原已刪除的群組、檢視可還原的群組，以及永久刪除 Azure Active Directory 中的群組"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 32d36ae96797a59bb47bf782ab038f21f231f046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="cdfc0-103">在 Azure Active Directory 中還原已刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="cdfc0-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="cdfc0-104">當您在 Azure Active Directory (Azure AD) 中刪除 Office 365 群組時，從刪除日起算，仍會保留已刪除的群組 30 天，但您看不見該群組。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="cdfc0-105">如此便能讓您視需要還原該群組及其內容。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="cdfc0-106">此功能專屬於 Azure AD 中的 Office 365 群組。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="cdfc0-107">無法針對安全性群組和發佈群組使用。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="cdfc0-108">請勿使用 `Remove-MsolGroup`，因為它會永久清除群組。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="cdfc0-109">一律使用 `Remove-AzureADMSGroup` 來刪除 O365 群組。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span> 

<span data-ttu-id="cdfc0-110">還原群組所需的權限可以是下列任一項：</span><span class="sxs-lookup"><span data-stu-id="cdfc0-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="cdfc0-111">角色</span><span class="sxs-lookup"><span data-stu-id="cdfc0-111">Role</span></span>  | <span data-ttu-id="cdfc0-112">權限</span><span class="sxs-lookup"><span data-stu-id="cdfc0-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="cdfc0-113">公司系統管理員、合作夥伴第 2 層支援，以及 InTune 服務管理員</span><span class="sxs-lookup"><span data-stu-id="cdfc0-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="cdfc0-114">可以還原任何已刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="cdfc0-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="cdfc0-115">使用者帳戶管理員和合作夥伴第 1 層支援</span><span class="sxs-lookup"><span data-stu-id="cdfc0-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="cdfc0-116">可以還原任何已刪除的 Office 365 群組，但指派給公司系統管理員角色的群組除外</span><span class="sxs-lookup"><span data-stu-id="cdfc0-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="cdfc0-117">User</span><span class="sxs-lookup"><span data-stu-id="cdfc0-117">User</span></span> | <span data-ttu-id="cdfc0-118">可以還原他們所擁有的任何已刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="cdfc0-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="cdfc0-119">檢視可供還原之已刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="cdfc0-119">View the deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="cdfc0-120">您可以使用下列 Cmdlet 來檢視已刪除的群組，以確認您感興趣的一或多個群組尚未被永久清除。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="cdfc0-121">這些 Cmdlet 屬於 [Azure AD PowerShell 模組](https://www.powershellgallery.com/packages/AzureAD/)。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="cdfc0-122">如需此模組的詳細資訊，請參閱 [Azure Active Directory PowerShell 第 2 版](/powershell/azure/install-adv2?view=azureadps-2.0)一文。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="cdfc0-123">執行下列 Cmdlet，以顯示租用戶中所有已刪除但仍可供還原的 Office 365 群組。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="cdfc0-124">或者，如果您知道特定群組的 objectID (而且可從步驟 1 中的 Cmdlet 取得)，請執行下列 Cmdlet 來確認該特定已刪除的群組尚未被永久清除。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="cdfc0-125">如何還原您所刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="cdfc0-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="cdfc0-126">一旦確認群組仍可供還原，即可使用下列其中一個步驟來還原已刪除的群組。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="cdfc0-127">如果群組包含文件、SP 網站或其他持續物件，則可能需要 24 小時，才能完全還原群組及其內容。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="cdfc0-128">執行下列 Cmdlet 來還原的群組及其內容。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="cdfc0-129">或者，可以執行下列 Cmdlet，永久移除已刪除的群組。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="cdfc0-130">如何知道此動作已完成？</span><span class="sxs-lookup"><span data-stu-id="cdfc0-130">How do you know this worked?</span></span>
<span data-ttu-id="cdfc0-131">若要確認您已順利還原 Office 365 群組，請執行 `Get-AzureADGroup –ObjectId <objectId>` Cmdlet 來顯示群組的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="cdfc0-132">完成還原要求之後：</span><span class="sxs-lookup"><span data-stu-id="cdfc0-132">After the restore request is completed:</span></span>
- <span data-ttu-id="cdfc0-133">群組將出現在 Exchange 的左側瀏覽列中</span><span class="sxs-lookup"><span data-stu-id="cdfc0-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="cdfc0-134">群組的計劃將出現在 Planner 中</span><span class="sxs-lookup"><span data-stu-id="cdfc0-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="cdfc0-135">任何 Sharepoint 網站及其所有內容都將可供使用</span><span class="sxs-lookup"><span data-stu-id="cdfc0-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="cdfc0-136">您可以從任何 Exchange 端點和支援 Office 365 群組的其他 Office 365 工作負載存取該群組</span><span class="sxs-lookup"><span data-stu-id="cdfc0-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="cdfc0-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdfc0-137">Next steps</span></span>
<span data-ttu-id="cdfc0-138">這些文章提供有關 Azure Active Directory 群組的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="cdfc0-139">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="cdfc0-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="cdfc0-140">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="cdfc0-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="cdfc0-141">管理群組的成員</span><span class="sxs-lookup"><span data-stu-id="cdfc0-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="cdfc0-142">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="cdfc0-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="cdfc0-143">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="cdfc0-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
