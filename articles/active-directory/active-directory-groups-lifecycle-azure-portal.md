---
title: "在 Azure Active Directory 中預覽 Office 365 群組到期日 | Microsoft Docs"
description: "如何設定 Azure Active Directory 中 Office 365 群組的到期日 (預覽)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: 8a43df84fd050d7b4bd8d937b8c55e744cb805d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="31911-103">設定 Office 365 群組到期日 (預覽)</span><span class="sxs-lookup"><span data-stu-id="31911-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="31911-104">您現在可以藉由設定到期日，對您選取任何 Office 365 群組管理 Office 365 群組的生命週期。</span><span class="sxs-lookup"><span data-stu-id="31911-104">You can now manage the lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="31911-105">一旦設定此到期日，如果這些群組的擁有者仍需要群組，則會要求他們續訂。</span><span class="sxs-lookup"><span data-stu-id="31911-105">Once this expiration is set, owners of those groups are asked to renew their groups if they still need the groups.</span></span> <span data-ttu-id="31911-106">未續訂的任何 Office 365 群組將會予以刪除。</span><span class="sxs-lookup"><span data-stu-id="31911-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="31911-107">群組擁有者或系統管理員可在 30 天內還原已刪除的任何 Office 365 群組。</span><span class="sxs-lookup"><span data-stu-id="31911-107">Any Office 365 group that was deleted can be restored within 30 days by the group owners or the administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="31911-108">您可以僅針對 Office 365 群組設定到期日。</span><span class="sxs-lookup"><span data-stu-id="31911-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="31911-109">設定已指派 Azure AD Premium 授權之 O365 群組所需要的到期日</span><span class="sxs-lookup"><span data-stu-id="31911-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="31911-110">為租用戶設定到期設定的系統管理員</span><span class="sxs-lookup"><span data-stu-id="31911-110">The administrator who configures the expiration settings for the tenant</span></span>
>   - <span data-ttu-id="31911-111">為此設定選取之群組的所有成員</span><span class="sxs-lookup"><span data-stu-id="31911-111">All members of the groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="31911-112">設定 Office 365 群組到期日</span><span class="sxs-lookup"><span data-stu-id="31911-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="31911-113">開啟其帳戶在 Azure AD 租用戶中為全域系統管理員的 [Azure AD 系統管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="31911-113">Open the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="31911-114">開啟 Azure AD，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="31911-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="31911-115">選取 [群組設定]，然後選取 [到期]，以開啟到期設定。</span><span class="sxs-lookup"><span data-stu-id="31911-115">Select **Group settings** and then select **Expiration** to open the expiration settings.</span></span>
  
  ![[到期] 刀鋒視窗](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="31911-117">在 [到期] 刀鋒視窗中，您可以：</span><span class="sxs-lookup"><span data-stu-id="31911-117">On the **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="31911-118">設定群組的存留期 (以天為單位)。</span><span class="sxs-lookup"><span data-stu-id="31911-118">Set the group lifetime in days.</span></span> <span data-ttu-id="31911-119">您可以選取其中一個預設值或自訂值 (應為 31 天或更多)。</span><span class="sxs-lookup"><span data-stu-id="31911-119">You could select one of the preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="31911-120">指定當群組沒有擁有者時應該傳送續訂和到期通知的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="31911-120">Specify an email address where the renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="31911-121">選取到期的 Office 365 群組。</span><span class="sxs-lookup"><span data-stu-id="31911-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="31911-122">您可以針對**所有** Office 365 群組啟用到期、從 Office 365 群組中選擇啟用對象，或選取 [無] 以停用所有群組的到期。</span><span class="sxs-lookup"><span data-stu-id="31911-122">You can enable expiration for **All** Office 365 groups, you can select from among the Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="31911-123">當您完成時，選取 [儲存] 會儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="31911-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="31911-124">如需如何下載及安裝 Microsoft PowerShell 模組以透過 PowerShell 設定 Office 365 群組之到期日的指示，請參閱 [Azure Active Directory V2 PowerShell 模組 - 公開預覽版本 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137)。</span><span class="sxs-lookup"><span data-stu-id="31911-124">For instructions on how to download and install the Microsoft PowerShell module to configure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="31911-125">這種電子郵件通知會在群組到期前 30 天、前 15 天和前 1 天傳送給 Office 365 群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="31911-125">Email notifications such as this one are sent to the Office 365 group owners 30 days, 15 days, and 1 day prior to expiration of the group.</span></span>

![到期電子郵件通知](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="31911-127">接著，群組擁有者可選取 [續訂群組] 以續訂 Office 365 群組，或可選取 [移至群組] 以查看成員和關於群組的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="31911-127">The group owner can then select **Renew group** to renew the Office 365 group, or can select **Go to group** to see the members and other details about the group.</span></span>

<span data-ttu-id="31911-128">當群組到期時，會在到期日隔天刪除群組。</span><span class="sxs-lookup"><span data-stu-id="31911-128">When a group expires, the group is deleted one day after the expiration date.</span></span> <span data-ttu-id="31911-129">這種電子郵件通知會傳送給 Office 365 群組擁有者，通知他們 Office 365 群組的到期日和後續刪除。</span><span class="sxs-lookup"><span data-stu-id="31911-129">An email notification such as this one is sent to the Office 365 group owners informing them about the expiration and subsequent deletion of their Office 365 group.</span></span>

![群組刪除電子郵件通知](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="31911-131">藉由選取 [還原群組] 或使用 PowerShell Cmdlet 可還原群組，如 [在 Azure Active Directory 中還原已刪除的 Office 365 群組] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal) 中所述。</span><span class="sxs-lookup"><span data-stu-id="31911-131">The group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="31911-132">如果您要還原的群組包含文件、SharePoint 網站或其他持續物件，則可能需要 24 小時，才能完全還原群組及其內容。</span><span class="sxs-lookup"><span data-stu-id="31911-132">If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="31911-133">部署到期設定時，可能會有一些群組已超過到期時間。</span><span class="sxs-lookup"><span data-stu-id="31911-133">When deploying the expiration settings, there might be some groups that are older than the expiration window.</span></span> <span data-ttu-id="31911-134">這些群組不會立即刪除，但會設定為 30 天後到期。</span><span class="sxs-lookup"><span data-stu-id="31911-134">These groups are not be immediately deleted, but are set to 30 days until expiration.</span></span> <span data-ttu-id="31911-135">第一封續訂通知電子郵件會在第一天發出。</span><span class="sxs-lookup"><span data-stu-id="31911-135">The first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="31911-136">例如，400 天前已建立群組 A，而且到期間隔設定為 180 天。</span><span class="sxs-lookup"><span data-stu-id="31911-136">For example, Group A was created 400 days ago, and the expiration interval is set to 180 days.</span></span> <span data-ttu-id="31911-137">您套用了到期設定，除非擁有者續訂群組 A，不然該群組就會在 30 天後刪除。</span><span class="sxs-lookup"><span data-stu-id="31911-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless the owner renews it.</span></span>
> * <span data-ttu-id="31911-138">刪除並還原動態群組時，會將其視為新群組，並根據規則重新填入。</span><span class="sxs-lookup"><span data-stu-id="31911-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according to the rule.</span></span> <span data-ttu-id="31911-139">此流程可能需要多達 24 小時的時間。</span><span class="sxs-lookup"><span data-stu-id="31911-139">This process might take up to 24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31911-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31911-140">Next steps</span></span>
<span data-ttu-id="31911-141">這些文章提供有關 Azure AD 群組的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="31911-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="31911-142">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="31911-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="31911-143">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="31911-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="31911-144">管理群組的成員</span><span class="sxs-lookup"><span data-stu-id="31911-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="31911-145">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="31911-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="31911-146">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="31911-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
