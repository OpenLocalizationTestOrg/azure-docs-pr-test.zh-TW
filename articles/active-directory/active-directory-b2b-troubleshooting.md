---
title: "Azure Active Directory B2B 共同作業 aaaTroubleshooting |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業常見問題的補救方式"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="2b2b9-103">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2b2b9-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="2b2b9-104">以下是 Azure Active Directory (Azure AD) B2B 共同作業常見問題的補救方式。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="2b2b9-105">我已新增外部使用者，但沒有看到這些全域通訊錄或 hello 人員選擇器中</span><span class="sxs-lookup"><span data-stu-id="2b2b9-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="2b2b9-106">在其中外部使用者不會填入 hello 清單中的情況下，hello 物件可能需要幾分鐘的時間 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="2b2b9-107">B2B 來賓使用者不會顯示在 SharePoint Online/OneDrive 人員選擇器中</span><span class="sxs-lookup"><span data-stu-id="2b2b9-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="2b2b9-108">hello 能力 toosearch hello SharePoint Online (SPO) 的人員選擇器中的現有 guest 使用者的預設 toomatch 舊版行為，是 OFF。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="2b2b9-109">您可以使用在 hello 租用戶和網站集合層級設定 'ShowPeoplePickerSuggestionsForGuestUsers' hello 啟用這項功能。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="2b2b9-110">您可以設定使用 hello 組 SPOTenant 和集 SPOSite cmdlet，讓成員 hello 功能 toosearch hello 目錄中的所有現有來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="2b2b9-111">Hello 租用戶範圍中的變更不會影響已佈建的 SPO 站台。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="2b2b9-112">已針對目錄停用邀請</span><span class="sxs-lookup"><span data-stu-id="2b2b9-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="2b2b9-113">如果您沒有 tooinvite 使用者權限，您會收到通知，請確認您的使用者帳戶是在使用者設定的授權的 tooinvite 外部使用者：</span><span class="sxs-lookup"><span data-stu-id="2b2b9-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="2b2b9-114">如果您最近有修改這些設定，或指派的 hello 來賓邀請者角色 tooa 使用者，可能有 15-60 分鐘的延遲之後 hello 變更才能生效。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="2b2b9-115">我受邀的 hello 使用者兌換期間收到錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="2b2b9-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="2b2b9-116">常見錯誤包括：</span><span class="sxs-lookup"><span data-stu-id="2b2b9-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="2b2b9-117">受邀者的管理員不允許在其租用戶中建立 EmailVerified 使用者</span><span class="sxs-lookup"><span data-stu-id="2b2b9-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="2b2b9-118">當邀請的使用者的組織使用 Azure Active Directory，但其中 hello 特定的使用者帳戶不存在 （例如，hello 使用者不存在於 Azure AD contoso.com）。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="2b2b9-119">contoso.com 的 hello 系統管理員可能已有原則防止使用者建立。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="2b2b9-120">hello 使用者必須檢查其管理員 toodetermine 與中，如果允許外部使用者。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="2b2b9-121">hello 外部使用者的系統管理員可能需要其網域中的 tooallow 電子郵件驗證使用者 (請參閱此[文章](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)上允許電子郵件驗證的使用者)。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="2b2b9-122">外部使用者不存在於同盟網域中</span><span class="sxs-lookup"><span data-stu-id="2b2b9-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="2b2b9-123">如果您使用同盟驗證 hello 使用者還沒有 Azure Active Directory 中，不得受邀 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="2b2b9-124">這個問題，請 hello tooresolve 外部使用者的系統管理員必須進行 hello 使用者帳戶 tooAzure Active Directory 同步處理。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="2b2b9-125">‘\#’ (通常是無效的字元) 如何與 Azure AD 同步？</span><span class="sxs-lookup"><span data-stu-id="2b2b9-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="2b2b9-126">「\#」 是 Azure AD B2B 共同作業或外部的使用者 Upn 中的保留的字元，因為 hello 受邀帳戶user@contoso.com變成 user_contoso.com#EXT@fabrikam.onmicrosoft.com。因此，\#中來自內部部署 Upn 中不允許有 toosign toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="2b2b9-127">新增外部使用者 tooa 同步處理群組時，我會收到的錯誤</span><span class="sxs-lookup"><span data-stu-id="2b2b9-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="2b2b9-128">外部使用者可以加入只太 「 指派 」 或者 「 安全性 」 群組和不屬於 toogroups 主控內部部署。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="2b2b9-129">我的外部使用者未收到電子郵件 tooredeem</span><span class="sxs-lookup"><span data-stu-id="2b2b9-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="2b2b9-130">hello 受邀者應洽詢其 ISP 或 hello 下列位址的垃圾郵件篩選器 tooensure 允許：Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="2b2b9-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="2b2b9-131">我發現該 hello 自訂訊息並不會隨附於邀請訊息有時</span><span class="sxs-lookup"><span data-stu-id="2b2b9-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="2b2b9-132">使用的隱私權法律 toocomply，我們的 Api，未包含的自訂訊息中的 hello 電子郵件邀請時：</span><span class="sxs-lookup"><span data-stu-id="2b2b9-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="2b2b9-133">hello 邀請者不在 hello 邀請租用戶的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="2b2b9-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="2b2b9-134">當應用程式服務主體傳送嗨邀請</span><span class="sxs-lookup"><span data-stu-id="2b2b9-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="2b2b9-135">如果重要 tooyou 這種情況下，您可以隱藏 API 邀請電子郵件，並透過您所選擇的 hello 電子郵件機制傳送。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="2b2b9-136">請參閱您的組織法律顧問 toomake 確定任何電子郵件傳送這種方式也符合隱私權法律。</span><span class="sxs-lookup"><span data-stu-id="2b2b9-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b2b9-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b2b9-137">Next steps</span></span>

<span data-ttu-id="2b2b9-138">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="2b2b9-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="2b2b9-139">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="2b2b9-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="2b2b9-140">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="2b2b9-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="2b2b9-141">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="2b2b9-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="2b2b9-142">hello hello B2B 共同作業邀請電子郵件項目</span><span class="sxs-lookup"><span data-stu-id="2b2b9-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="2b2b9-143">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="2b2b9-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="2b2b9-144">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="2b2b9-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="2b2b9-145">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="2b2b9-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="2b2b9-146">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="2b2b9-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="2b2b9-147">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="2b2b9-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="2b2b9-148">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="2b2b9-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="2b2b9-149">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="2b2b9-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
