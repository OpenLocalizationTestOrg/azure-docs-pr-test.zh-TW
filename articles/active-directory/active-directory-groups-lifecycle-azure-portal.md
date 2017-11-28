---
title: "aaaPreview Office 365 群組在 Azure Active Directory 中的到期日 |Microsoft 文件"
description: "在 Azure Active Directory （預覽） tooset for Office 365 的到期組成群組的方式"
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
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="d3e5b-103">設定 Office 365 群組到期日 (預覽)</span><span class="sxs-lookup"><span data-stu-id="d3e5b-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="d3e5b-104">您現在可以藉由設定到期日，對您選取任何 Office 365 群組管理 Office 365 群組 hello 生命週期。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="d3e5b-105">這些群組的擁有者一旦設定此期限，已要求 toorenew 其群組，如果它們仍然需要 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="d3e5b-106">未續訂的任何 Office 365 群組將會予以刪除。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="d3e5b-107">可以還原已刪除的任何 Office 365 群組的 30 天內，hello 群組擁有者或 hello 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="d3e5b-108">您可以僅針對 Office 365 群組設定到期日。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="d3e5b-109">設定已指派 Azure AD Premium 授權之 O365 群組所需要的到期日</span><span class="sxs-lookup"><span data-stu-id="d3e5b-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="d3e5b-110">hello 系統管理員設定 hello hello 租用戶的到期設定</span><span class="sxs-lookup"><span data-stu-id="d3e5b-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="d3e5b-111">選取此設定的 hello 群組的所有成員</span><span class="sxs-lookup"><span data-stu-id="d3e5b-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="d3e5b-112">設定 Office 365 群組到期日</span><span class="sxs-lookup"><span data-stu-id="d3e5b-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="d3e5b-113">開啟 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)與 Azure AD 租用戶中的全域系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="d3e5b-114">開啟 Azure AD，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="d3e5b-115">選取**群組設定**，然後選取 **到期**tooopen hello 逾期設定。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![[到期] 刀鋒視窗](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="d3e5b-117">在 hello**到期**刀鋒視窗中，您可以：</span><span class="sxs-lookup"><span data-stu-id="d3e5b-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="d3e5b-118">設定以天為單位的 hello 群組存留時間。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="d3e5b-119">您可以選取其中一個 hello 預設值或自訂的值 （應為 31 天或更多）。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="d3e5b-120">指定的群組有沒有擁有者時，傳送 hello 更新與到期通知電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="d3e5b-121">選取到期的 Office 365 群組。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="d3e5b-122">您可以啟用到期日**所有**Office 365 群組中，您可以從 hello Office 365 群組中選取，或者您選取**無**停用所有群組的到期日。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="d3e5b-123">當您完成時，選取 [儲存] 會儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="d3e5b-124">如需 toodownload 並安裝 hello Microsoft PowerShell 模組 tooconfigure 到期日，Office 365 群組透過 PowerShell 的指示，請參閱[Azure Active Directory V2 PowerShell 模組-公開預覽版本 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137)。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="d3e5b-125">Toohello Office 365 群組擁有者 30 天，15 天和 tooexpiration hello 群組的 1 日之前，會傳送電子郵件通知，例如這一個。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![到期電子郵件通知](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="d3e5b-127">然後可以選取 hello 群組擁有者**更新群組**toorenew hello Office 365 群組，或者也可以選取**移 toogroup** toosee hello 成員以及其他詳細資料 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="d3e5b-128">當群組到期時，hello 群組將刪除 hello 到期日期後一天。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="d3e5b-129">這種電子郵件通知會傳送告知 hello 到期和後續刪除其 Office 365 群組 toohello Office 365 群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![群組刪除電子郵件通知](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="d3e5b-131">可選取還原 hello 群組**還原群組**或 Azure Active Directory 中還原已刪除的 Office 365 群組] 中所述使用 PowerShell cmdlet (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="d3e5b-132">如果您要還原的 hello 群組包含文件、 SharePoint 網站或其他持續性的物件，它可能會佔用 too24 小時 toofully 還原 hello 群組和其內容。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="d3e5b-133">當部署 hello 到期日設定，可能會有超過 hello 到期視窗部分群組。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="d3e5b-134">這些群組不會被立即刪除，但設定 too30 到期之前的天數。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="d3e5b-135">hello 第一個更新通知電子郵件會在一天之內送出。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="d3e5b-136">例如，群組 A 已建立 400 天前，並設定 hello 到期間隔 too180 天。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="d3e5b-137">當您套用到期日設定時，群組 A 會有 30 天之後會被刪除，, 除非 hello 擁有者更新它。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="d3e5b-138">當刪除並還原動態群組時，它被視為新的群組並重新填入相應 toohello 規則。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="d3e5b-139">此程序可能佔用 too24 小時。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3e5b-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3e5b-140">Next steps</span></span>
<span data-ttu-id="d3e5b-141">這些文章提供有關 Azure AD 群組的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="d3e5b-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="d3e5b-142">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="d3e5b-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d3e5b-143">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="d3e5b-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="d3e5b-144">管理群組的成員</span><span class="sxs-lookup"><span data-stu-id="d3e5b-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="d3e5b-145">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="d3e5b-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="d3e5b-146">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="d3e5b-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
