---
title: "Azure Active Directory 中的 aaaRestore 已刪除的 Office 365 群組 |Microsoft 文件"
description: "Toorestore 已刪除的群組、 檢視可還原的已群組和 permamnently 刪除 Azure Active Directory 中的群組"
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
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="fdd8c-103">在 Azure Active Directory 中還原已刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="fdd8c-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="fdd8c-104">當您刪除 hello Azure Active Directory (Azure AD) 中的 Office 365 群組時，hello 刪除群組為保留，但看不到 30 天內從 hello 刪除日期。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="fdd8c-105">這是可以還原 hello 群組和其內容，如有需要。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="fdd8c-106">此功能會受到限制專門 tooOffice 365 Azure AD 中的群組。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="fdd8c-107">無法針對安全性群組和發佈群組使用。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="fdd8c-108">請勿使用`Remove-MsolGroup`因為永遠會清除 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="fdd8c-109">一律使用`Remove-AzureADMSGroup`toodelete O365 群組。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="fdd8c-110">hello 權限所需 toorestore 群組可以是 hello 下列任何一項：</span><span class="sxs-lookup"><span data-stu-id="fdd8c-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="fdd8c-111">角色</span><span class="sxs-lookup"><span data-stu-id="fdd8c-111">Role</span></span>  | <span data-ttu-id="fdd8c-112">權限</span><span class="sxs-lookup"><span data-stu-id="fdd8c-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="fdd8c-113">公司系統管理員、合作夥伴第 2 層支援，以及 InTune 服務管理員</span><span class="sxs-lookup"><span data-stu-id="fdd8c-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="fdd8c-114">可以還原任何已刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="fdd8c-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="fdd8c-115">使用者帳戶管理員和合作夥伴第 1 層支援</span><span class="sxs-lookup"><span data-stu-id="fdd8c-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="fdd8c-116">可以還原任何已刪除的 Office 365 群組，除了那些指派 toohello 公司系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="fdd8c-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="fdd8c-117">User</span><span class="sxs-lookup"><span data-stu-id="fdd8c-117">User</span></span> | <span data-ttu-id="fdd8c-118">可以還原他們所擁有的任何已刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="fdd8c-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="fdd8c-119">檢視 hello 刪除可用的 toorestore Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="fdd8c-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="fdd8c-120">hello 下列指令程式可以使用的 tooview hello 刪除群組 tooverify hello 其中一個，或您感興趣的一不尚未永久清除。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="fdd8c-121">這些 cmdlet 屬於 hello [Azure AD PowerShell 模組](https://www.powershellgallery.com/packages/AzureAD/)。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="fdd8c-122">可以找到此模組的詳細資訊，在 hello [Azure Active Directory PowerShell 版本 2](/powershell/azure/install-adv2?view=azureadps-2.0)發行項。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="fdd8c-123">執行下列 cmdlet toodisplay 刪除所有 Office 365 租用戶中的群組仍然可以使用 toorestore hello。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="fdd8c-124">或者，如果您知道某特定群組的 hello objectID （而且您可以從步驟 1 中的 hello cmdlet 取得），執行下列 cmdlet tooverify 的 hello 特定的已刪除的群組的 hello 不尚未已永久清除。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="fdd8c-125">如何 toorestore 已刪除的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="fdd8c-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="fdd8c-126">一旦您確認該 hello 群組是 toorestore 仍然可以使用時，請使用其中一個步驟的 hello 還原 hello 刪除群組。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="fdd8c-127">如果 hello 群組包含文件、 預存程序的網站或其他持續性的物件，它最多可能需要 too24 小時 toofully 還原為群組和其內容。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="fdd8c-128">執行 hello 下列 cmdlet toorestore hello 群組和其內容。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="fdd8c-129">或者，hello 下列 cmdlet 可以執行 toopermanently 移除 hello 刪除群組。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="fdd8c-130">如何知道此動作已完成？</span><span class="sxs-lookup"><span data-stu-id="fdd8c-130">How do you know this worked?</span></span>
<span data-ttu-id="fdd8c-131">您已成功還原將 Office 365 群組執行 hello tooverify `Get-AzureADGroup –ObjectId <objectId>` hello 群組 cmdlet toodisplay 資訊。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="fdd8c-132">Hello 還原之後完成的要求：</span><span class="sxs-lookup"><span data-stu-id="fdd8c-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="fdd8c-133">hello 群組會出現在交換上的 hello 左瀏覽列</span><span class="sxs-lookup"><span data-stu-id="fdd8c-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="fdd8c-134">hello 計劃 hello 群組會出現在規劃</span><span class="sxs-lookup"><span data-stu-id="fdd8c-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="fdd8c-135">任何 Sharepoint 網站及其所有內容都將可供使用</span><span class="sxs-lookup"><span data-stu-id="fdd8c-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="fdd8c-136">您可以從任何 hello 交換端點和支援 Office 365 群組的其他 Office 365 工作負載存取 hello 群組</span><span class="sxs-lookup"><span data-stu-id="fdd8c-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="fdd8c-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdd8c-137">Next steps</span></span>
<span data-ttu-id="fdd8c-138">這些文章提供有關 Azure Active Directory 群組的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="fdd8c-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="fdd8c-139">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="fdd8c-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="fdd8c-140">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="fdd8c-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="fdd8c-141">管理群組的成員</span><span class="sxs-lookup"><span data-stu-id="fdd8c-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="fdd8c-142">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="fdd8c-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="fdd8c-143">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="fdd8c-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
